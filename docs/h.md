# Exercise H

## Task

Native contract = Raw qty value
Base asset units = the amount of underlying represented by the contracts
    qty * qty multiplier
Quote currency units = Values of the trade in the quote currency. Ie USDT
    base asset qty * price

Timestamps in unix time, can cast to datetime if we want

Native contracts 8.959318e6

Base asset units 895.9318

Quote currency units 6.6923e7

## Validation

Query api and use part of response which contains t=1779537600 as that is the hour we want to look at

Our native contracts - 8959318
Gate v - 8959318

Our quote USDT - 66,923,451.09224
Gate sum - 66,923,451.09224

Matches exactly