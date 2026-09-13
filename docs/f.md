# Exercise F

Prices are USDT per ETH quantities are ETH

## Data quality

Exercise E doesn't exist (missing part of sequence)

Bid/ask quantities decimal which is ok for crypto spot markets

0 Null cells
No duplicate seq ids
No dupes at all

Plotted data looks okay

No negative bid/ask values

No crossed or locked books

Very tight and stable spread
    can flag p99 if we want. telemetry i guess

Ingress ts not monotonic relative to seq id. 
    32 reversals, max 17us

We cannot measure capture latency as we have no publish ts or transaction ts

Clean file. Not much to add
    