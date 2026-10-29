# KO-PEP Pairs Trading Backtest

This project tests whether Coca-Cola (KO) and PepsiCo (PEP) log prices were cointegrated bewteen 2015 and 2021 and backtests a simple mean-reversion strategy between 2022 and 2025.


## Performance Visualisations

### Price Series & Cointegration Check
The strategy operates on daily adjusted log prices for KO and PEP spanning 2015 to 2025:
![KO and PEP Prices}(prices.png)

### In-Sample Spread Estimation (2015-2021)
During the in-sample period, an OLS regression estimates the stationary spread relationship $S_t = \ln(P_{KO}) - \alpha - \beta \ln(P_{PEP})$:
![Training Spread](training_spread.png)

## Key Metrics

| Metric | Value |
| --- | --- |
| Cointegration statistic | -3.5764 |
| Cointegration p-value | 0.0262 |
| Total Cumulative P&L Units | -0.0043 |
| Max Drawdown Units | -0.1323 |
| Total Trades Executed | 3 |

## Method
- Downloaded the daily adjusted closing prices using 'yfinance' data (Yahoo Finance)
- Converted the prices into log prices
- Tested for cointegration using the Engle-Granger test
- Estimated a relationship between KO and PEP using OLS
- Traded the standardised spread using ±2 standard-deviation entry thresholds
- Included a 10 basis-point transaction cost per position change





## Results

