# Exercise D

Prices are USDT per BTC quantities are BTC

## Reconstruction

Transaction ts fully null
Check lists with unequal price/quantity sizes

Snapshot always false

I see null values when looking at the data tho (in parquet viewer). In ask_qts, etc
    Empty lists are not null values!
    Can mean no updates for that side
    flag 

Negative values (in the lists). pass
Publish ts monotonic relative to seq id, pass

find all crossed messages using inside of the lists
ony one- [98502143047] flag

### Snapshot = full order book at a point in time
### Classify snapshot as >p99 count(ask prices+bid prices)
#### flag as "snapshot esque", 183 total inferred snapshots

214 crossed books and min spread pretty bad

plot that, looks great mostly. massive gap at 14:15

[98502143047] is one of these naturally. is it breaking everything
its the first row of that trench. so probably
remove it

plot looks good now
crossed rows 0

__However, I am REJECTING this approach after my second attempt__

## Second try - d_secondtry.ipynb

Decided to do this again, without the inferred snapshots and just by removing the bad row
It also reconstructs, and with more price points (3509) compared to the first try, (537)

I believe this was the intended solution
Either way, it is a partial replay with no real reset snapshot. We cannot consider this correct
