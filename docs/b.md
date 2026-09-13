# Exercise B

## Data Quality

Looked at data first and saw transaction and publish ts are all NULL (double checked in code)
Cannot compute ingress_ts - publish_ts latency because publish_ts is fully null
So we can only rely on seq id for ordering
    6 hours and 13 minutes worth of data looking at the ingress timestamps


bid_price and bid_qty missing for 1540 rows 
these rows look concentrated at the end of the file, last ~90 mins
    missing data or one sided?
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

Check spread outliers *for the 2 sided rows
    p99 0.133%, max 0.270%
    very tame. not even going to flag

check out lowest bids
    looks ok
check out highest bids
    looks ok
check out highest asks
    there are 3 which really stand out at 0.0097 ask qty and a significantly higher ask price
        manually flagged. prices return to normal on the next update
check out lowest asks
    looks ok


microprice = weighted mid that uses the size on each side of the book

mid = (bid_price + ask_price) / 2
microprice = (bid_price * ask_qty + ask_price * bid_qty) / (bid_qty + ask_qty)

we can only calcualte this for where we have both sides.
so for the 1540 rows with no bid price/bid qty it is n/a

Plotted, and you can see the missing part at the end


 