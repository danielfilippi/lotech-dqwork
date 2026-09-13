# Exercise C

Prices are USD per share, quantities are shares

## Data Quality

Different symbols. There is no "S|" prefixing them, though, for what it's worth
Count them first, 18. Filename says 20

Plot their mids. Ok

Looks ok already and 0 null cells

Publish ts, transaction ts, ingress ts monotonic relative to seq id? and for each symbol?
Y N N
quantify the reversals
capture timestamps reversals less severe
transaction timestamps reverse 45k times, by up to 218ms


Exact repeated rows not found
There are repeated quotes however, ~322k
    not confirmed duplicate events

Lets look at (ingress ts - publish ts) latency
    max is ~2.9 seconds
    lets look at all rows where latency >1 second
        they seem to almsot all be captured at 15:27. and it is affecting 17 instruments
        some kind of shared issue here. lets flag these rows
            we would like to find out the root cause though somehow

looking at the publish ts - transaction ts latency for 15:26, 27 and 28
    we see a concentration at 27 again
    some kind of congestion occurring maybe? but we cant determine anything with what we have


1030 Crossed book
26814 Locked
get it by instrument as well
flag

negative numbers pass

spread outliers
    standout:
    LRGE-USD:SPOT
        p99 spread 0.524%
        max spread 11.387%

    relatively wide:
    ATRO-USD:SPOT
        p99 0.949%
        max 1.183%

    QMOM-USD:SPOT
        p99 0.283%
        max 0.898%

    TIGO-USD:SPOT
        p98 0.399%
        max 0.792%

most of the larger/liquid ones look fine
QQQ max 0.023%
AAPL max 0.039%
NVDA max 0.058%
AMZN max 0.075%
MSFT max 0.093%

flag p99 outliers per symbol. then count

