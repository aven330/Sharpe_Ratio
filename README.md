# Sharpe Ratio Analysis

## Akhil Venkat

---

## What is the Sharpe Ratio?

The Sharpe Ratio measures the average return you earned above the risk-free rate per unit of total risk in an attempt to quantify the given success of any investment in comparison to a risk-free investment.

## Why is the Sharpe Ratio Usefull?

The Sharpe Ratio allows an investor to differentiate which investments returns were the most risk efficent compared to something more concrete like a Treasury bill or bond. And since it is a ratio, of annualized values, you can compare it to any investment allowing you to make more informed decisions.

## How is it calculated?


<img width="625" height="245" alt="Screenshot 2026-04-22 at 11 14 04 PM" src="https://github.com/user-attachments/assets/95dd9e25-352b-4fe3-8e01-bcf7a15ea853" />


- Return of Portfolio = **`annualized_returns`**
- Risk-Free Rate = **`risk free rate`**
- Standard Deviation of the Portfolio's Excess Return = **`annualized volatility`**

- **`annualized_returns`** -> returns of a investment computed yearly for better comparison. (Mean of daily returns multiplied by number of periods in the time horizon)
- **`risk free rate`** -> rate at which an investment is considered to be risk free.
- **`annualized volatility`** -> the variance of an invesments returns computed yearly for better comparison. (Standard Deviation of Returns mulitplied by sqrt of number of periods in the time horizon)

## Creating the function
```
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04)
```    

- ### Accessing the Data
For this task I utilized the crowdsource library yfinance which is an open-source tool that uses Yahoo's publicly available APIs
```
import yfinance as yf
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04):
    data = pd.DataFrame(yf.download(ticker_symbols, start = start, end = end, auto_adjust = True))
```
- ### Obtaining the Daily Returns
Here I queried the closing data from the dataframe and used the ```.pct_change()``` function which calculates the percentage differnce from each day and the dropped all null values. This is neccessary since the first day has no percent change because there is no entry before it.
```
# Extracting Closing Data
closing_data = data['Close'].dropna()
# Evaluating Daily Returns
daily_returns = closing_data.pct_change().dropna()
```
