# Exercise C

## Data Quality

Different symbols.
Count them first, 18. Filename says 20

Plot their mids. Ok

Looks ok already and 0 nulls

Publish ts, transaction ts, ingress ts monotonic relative to seq id? and for each symbol?
Y N N
Behaves perfectly here too

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

this data looks okay. you dont really have to use my flags but you should probably have something monitoring them and triggering alerts

happy to continue