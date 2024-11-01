---
title: Time Series
date: 10-31-2024
---

Time series is essentially data that is recorded in time order. In nearly all cases, the data includes
a timestamp with one or more data points being collected at that time. Time series data is commonly
seen in fields that analyze trends over time.

### Characteristics

- **Trends**: Drifting up or down
- **Seasonality**: Regularly occurring
- **Cyclic**: Exhibits a rise and fall at unknown intervals 
- **Stationary**: Mean & std dev is constant
  - Trend-stationary is also possible

## Tests

- [[math/fields/finance/topics/timeseries/engle-granger-method|Engle Granger Method]]
  - Useful for determining if there's a correlation between two processes
- [[math/fields/finance/topics/timeseries/kpss-test|KPSS test]]
  - Hypothesis test to determine if the process is stationary or trend-stationary

[^1]: [YouTube - Time Series Modeling and Analysis Playlist](https://www.youtube.com/watch?v=-r7wB9DJtiU&list=PL3N9eeOlCrP5cK0QRQxeJd6GrQvhAtpBK)
