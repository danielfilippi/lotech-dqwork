# Exercise D

## Data Quality

Transaction ts fully null
Snapshot always false

I see null values when looking at the data tho (in parquet viewer). In ask_qts, etc
    Empty lists are not null values!
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
