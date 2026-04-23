# Sharpe Ratio Analysis

## Akhil Venkat

---


## What is the Sharpe Ratio?

The Sharpe Ratio measures the average return you earned above the risk-free rate per unit of total risk in an attempt to quantify the given success of any investment in comparison to a risk-free investment.

## Why is the Sharpe Ratio Usefull?

The Sharpe Ratio allows an investor to differentiate which investments returns were the most risk efficent compared to something more concrete like a Treasury bill or bond. And since it is a ratio, of annualized values, you can compare it to any investment allowing you to make more informed decisions.

## How is it calculated?

<img width="1090" height="442" alt="Screenshot 2026-04-22 at 9 15 38 PM" src="https://github.com/user-attachments/assets/667e0252-6cc4-4756-a7ce-79e5624e3a35" />


- return of portfolio = annualized returns
- risk-free rate = risk-free rate
- standard deviation of the portfolio's excess return = annualized volatility

- **`annualized_returns`** -> returns of a investment computed yearly for better comparison. (Mean of daily returns multiplied by number of periods in the time horizon)
- **`risk free rate`** -> rate at which an investment is considered to be risk free.
- **`annualized volatility`** -> the variance of an invesments returns computed yearly for better comparison. (Standard Deviation of Returns mulitplied by sqrt of number of periods in the time horizon)

## Creating the function
```
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04)
```

### Accessing the Data
For this task I utilized the crowdsource library, yfinance which pulls data from yahoo finance.

```
import yfinance as yf
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04):
    data = pd.DataFrame(yf.download(ticker_symbols, start = start, end = end, auto_adjust = True))
```
