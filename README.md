# Sharpe Ratio Analysis

### Akhil Venkat
\usepackage{amsmath}
\usepackage{mathtools}

---

## What is the Sharpe Ratio?

The Sharpe Ratio measures the average return earned in excess of the risk-free rate per unit of total risk in an attempt to quantify the given success of any investment in comparison to a risk-free investment.

## How is it calculated?

Sharpe Ratio = $\frac{annualized returns - risk free rate}{annualized volatility}$
$R_{p}$
$R_{f}$
$k_{\sigma}$

- **`annualized_returns`** -> returns of a investment computed yearly for better comparison. (Mean of daily returns multiplied by number of periods in the time horizon)
- **`risk free rate`** -> rate at which an investment is considered to be risk free.
- **`annualized volatility`** -> the variance of an invesments returns computed yearly for better comparison. (Standard Deviation of Returns mulitplied by sqrt of number of periods in the time horizon)

## Why is the Sharpe Ratio Usefull?

The Sharpe Ratio allows an investor to quantify how much $\frac{1}{5}$.

## Accessing the Data

```
import yfinance as yf
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04):
    data = pd.DataFrame(yf.download(ticker_symbols, start = start, end = end, auto_adjust = True))
```
