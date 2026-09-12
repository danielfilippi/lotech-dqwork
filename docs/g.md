# Exercise G

## Data Quality

Small file

Other data completely empty
Timestamps are integers not DateTimes
    Casted to timestamps

Plotted data looks okay
    Range is plausible
    No obvious spikes or trenches
    Trades are clustered
    Buy/sell behaviour looks natural

(Ingress ts - publish ts) latency looks very good. No anomalies found
    Can flag p99s if we want to monitor

0 total duplicate rows but.
321 duplicate trade ids, half of the file
    Looking at one, it is indeed the same trade repeated twice
    If we look for dupes on (trade id, price, qty and side). We see 321 rows / 642 rows involved
    So these are duplicate trade events 
        flag these (either after first occurrence, or just any trade that is duplicated at all) I chose any duplicated trade. So all rows are flagged here

copy 0 is published almost immediately after transaction ts  ~1-5ms
copy 1 published again later  ~18-106ms

Median gap between duplicate publish ts is 49ms, with a max of 104ms