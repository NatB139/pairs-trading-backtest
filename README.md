# KO-PEP Pairs Trading Backtest

This project tests whether Coca-Cola (KO) and PepsiCo (PEP) log prices were cointegrated bewteen 2015 and 2021 and backtests a simple mean-reversion strategy between 2022 and 2025.


## Performance Visualisations

### Price Series & Cointegration Check
The strategy operates on daily adjusted log prices for KO and PEP spanning 2015 to 2025:
![KO and PEP Prices](prices.png)

### In-Sample Spread Estimation (2015-2021)
During the in-sample period, an OLS regression estimates the stationary spread relationship $S_t = \ln(P_{KO}) - \alpha - \beta \ln(P_{PEP})$:
![Training Spread](training_spread.png)

### Out-of-Sample Trading Signals (2022–2024)
Using the in-sample mean ($\mu$) and standard deviation ($\sigma$), out-of-sample normalized Z-scores trigger mean-reversion trades:

![Trading Signals](signals.png)

### Out-of-Sample Cumulative P&L
Cumulative returns incorporating a fixed transaction cost penalty per trade turnover:

![Equity Curve](equity_curve.png)

--

## Mathematical Framework & Methodology

### 1. Cointegration Test
Applied the Engle-Granger two-step cointegration test ('statsmodels.tsa.stattools.coint') on the in-sample log prices:
$$\text{Null Hypothesis } (H_0): \text{The log price series are NOT cointegrated}$$

A statistically significant $p \le 0.05$ rejects $H_0$, verifying that linear combinations of the asset prices form a stationary series.

### 2. Hedge Ratio & Spread Model
Ordinary Least Squares (OLS) regression extracts parameters $\alpha$ and $\beta$:
$$\ln(P_{KO, t}) = \alpha + \beta \ln(P_{PEP, t}) + \epsilon_t$$

The spread $S_t$ and noramlised z-score $Z_t$ are evaluated as:
$$S_t = \ln(P_{KO, t}) - \alpha - \beta \ln(P_{PEP, t})$$
$$Z_t = \frac{S_t - \mu_{train}}{\sigma_{train}}$$

### 3. Execution Rules
Positions are shifted by 1 period ($t+1$) to avoid look-ahead bias:
- **Long Spread Entry:** $Z_t \le -2.0$ (Buy KO, Sell PEP)
- **Short Spread Entry:** $Z_t \ge +2.0$ (Sell KO, Buy PEP)
- **Long Spread Exit:** $Z_t \ge -0.5$
- **Short Spread Exit:** $Z_t \le +0.5$


## Key Metrics

| Metric | Value |
| --- | --- |
| Cointegration statistic | -3.5764 |
| Cointegration p-value | 0.0262 |
| Total Cumulative P&L Units | -0.0043 |
| Max Drawdown Units | -0.1323 |
| Total Trades Executed | 3 |

