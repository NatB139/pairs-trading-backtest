# KO-PEP Pairs Trading Backtest

This project tests whether Coca-Cola (KO) and PepsiCo (PEP) log prices were cointegrated bewteen 2015 and 2021 and backtests a simple mean-reversion strategy between 2022 and 2025.

## Method
- Downloaded the daily adjusted closing prices using 'yfinance' data (Yahoo Finance)
- Converted the prices into log prices
- Tested for cointegration using the Engle-Granger test
- Estimated a relationship between KO and PEP using OLS
- Traded the standardised spread using ±2 standard-deviation entry thresholds
- Included a 10 basis-point transaction cost per position change

## Results

