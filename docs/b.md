# Exercise B

## Data Quality

Looked at data first and saw transaction and publish ts are all NULL (double checked in code)
Cannot compute ingress_ts - publish_ts latency because publish_ts is fully null
So we can only rely on seq id for ordering
    20 minutes worth of data looking at the ingress timestamps


bid_price and bid_qty missing for 1540 rows 
Ask side is complete
    Looks like there is genuine one sided liquidity here or missing bid side capture (Flag)

No identical row dupes
No duplicate seq ids
No duplicate ingress timestamps
No repeated bbo states

Overall not enough evidence for duped data

Ingress monotonic relative to seqid. pass

No crossed or locked book rows

Negative numbers check. Pass

Check spread outliers
    p99 0.133%, max 0.270%
    very tame. not even going to flag


microprice = weighted mid that uses the size on each side of the book

mid = (bid_price + ask_price) / 2
microprice = (bid_price * ask_qty + ask_price * bid_qty) / (bid_qty + ask_qty)

Plotted


