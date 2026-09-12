# Exercise A

# Individual file checks

Comprehensive and boring is key

## TOP OF BOOK - a_topofbook_initial

Dedupe fully duplicated rows, nothing changed

No dupe seq ids
Descending Seq ids spotted
    just order by seq id

Lots of timestamp dupes
    Ingress, our own system, not necessarily bad. ~75% of rows involved
    transaction/publish, possible if timestamps are batched. Same number of rows involved too looks intentional. Or from the same venue ?

No consecutive repeated BBO states

There are rows where we see the same exact data, but different ingress tss and sequence id
    flag any identical occurrence after the first

Even after ordering by seq id.  the timestamps are not monotonic
    For basic ordering use seq id. For timing analysis, keep timestamp order anomalies flagged
We see that publish and transaction ts are the worst offenders
    They reverse 55 times with a max of ~89 mins
ingress  isnt as severe

Negative number check, pass
Timestamp sanity, pass

High (ingress_ts - publish_ts) latency at times
    Flag p95/p99 rows. 
    Flag >1s in case of any latency sensitive use cases

Checking these >1s delay rows we see that 58/59 of them are actually repeated data
    repeated a quotes timestamps, prices and quantities

Few null values present. In bid/ask price/quantity
    Classify these rows as it could just be a one sided market

71 Crossed book rows (bid>ask) Flag and probably exclude these from future calculations
112 Locked book rows (bid=ask) Flag

Spread outliers
    Measured spread as a % of mid 
    Using p99 as a threshold, 812 rows flagged as unusual
    p99 spread = 0.15%, Max spread = 6.42%
    Flag rows

Find implausible price jumps
    identify biggest % movers
    look for any jumps/reversals around the top move
        95072669 looks strange
            crossed book
            qtys collaps from millions, to 6 and 5
            pruces return to 25.92/25.94 a second later
            already flagged by crossed book flag though, so lets rerun but exclude quotes we've already caught
        we see a candidate at 6:08 where quantities collapse again, and then things are restored 163ms later
            manuallyl flagged as suspicious

Time gaps in charted data

After some research on the HKEX (Time in UTC)

Pre-open auction:     01:00-01:30 Visible
Morning continuous:   01:30-04:00
Lunch break:          04:00-05:00 Visible
Afternoon continuous: 05:00-08:00
Closing auction:      08:00-08:10

Flag rows

"before_open"	55036... Why? 

wow. integer overflow
    5:45 was being classified as pre_open
        calculated minute mustve been less than 90 but
        5:45 = 5*60 + 45 (345)

    rows at 8:08 classified as before_open.
        calculated value should be <60
        8:08 = 488

        In polars, dt.hour can produce int8s (no larger than 127)
        so we cast it to int32

        (probably) not an intended data quality issue but an important thing to remember nonetheless


Prior chart with selected flags excluded
cleaner / visually stable 



## Trades - a_trades_initial

Dedupe fully duplicated rows, nothing changed.

No dupe trade ids (trade id is also a string here and not an int)
    Cast to int. No fails
    Many descending ids
    Seq = sequence, indicating ordering. The word "trade" does not tell me with confidence that it is attempting to guarantee correct ordering
    Leaning towards ordering by timestamp

Timestamp dupe behaviour similar to top of book data
    No publish < transation cases
    Different amount of transaction and publish ts dupes
        publish_ts - transaction_ts - the amount of time it took for an executed trade to be published.
        transaction always equals publish (unless its null)
    Lots of missing transaction_ts
    publish ts are complete. __So yes, order by publish ts__

Repeated identical trades exist at the same timestamps, but trade_id remains unique.
    Cant classify these as duplicate trades, could just be the identical transactions

No evidence of duped data

Negative number checks pass

Timestamp sanity pass

Good looking (ingress_ts - publish_ts) latency stats
    Flag p95/p99 rows still. 
    Flag >1s even though none exist. But if they ever do.....

No nulls except for transation nulls, and other_data fully null
    Core fields populated

Only "buy" side
    Intentional? Or not? I would need clarification here

Take a look at the lowest price trades
    Found three suspicious trades (2754, 2755, 5588) priced well below neighbouring trades, with prices returning shortly afterwards. review these

# Joined data checks - a_joined

Joined and charted to illustrate the filtering

Apply all our flags and exlude these from the charting, 
    the remaining trades sit cleanly inside the bbo. 
    This suggests our flags are isolating unusual records while preserving the normal market structure of the day

But we should remember that this does not prove every retained row is correct.