# Sharpe Ratio Analysis

## Akhil Venkat

---

## What is the Sharpe Ratio?

The Sharpe Ratio measures the average return you earned above the risk-free rate per unit of total risk in an attempt to quantify the given success of any investment in comparison to a risk-free investment.

## Why is the Sharpe Ratio Usefull?

The Sharpe Ratio allows an investor to differentiate which investments returns were the most risk efficent compared to something more concrete like a Treasury bill or bond. And since it is a ratio, of annualized values, you can compare it to any investment allowing you to make more informed decisions.

## Creating the function
```
def Sharpe(ticker_symbols, start, end, risk_free_rate = 0.04):
   ...
```    

### Accessing the Data
For this task I utilized the crowdsource library yfinance which is an open-source tool that uses Yahoo's publicly available APIs
```
import yfinance as yf

data = pd.DataFrame(yf.download(ticker_symbols, start = start, end = end, auto_adjust = True))
```
### Daily Returns
Here I queried the closing data from the dataframe and used the ```.pct_change()``` function which calculates the percentage differnce from each day. Then I made sure to dropp all null values since the first day has no percent change because there is no entry before it.
```
# Extracting Closing Data
closing_data = data['Close'].dropna()
# Evaluating Daily Returns
daily_returns = closing_data.pct_change().dropna()
```
### Simple Returns and Log Returns
- **`Simple Returns`**: I indexed the most recent closing value and subtracted the first closing value all over the first closing value to get the returns for the given time frame.
- **`Log Returns`**: I took the log of the most recent closing value divided by the first closing value to get the log returns for the given time frame.
```
# Evaluating Simple Returns
simple_returns = (closing_data.iloc[-1] - closing_data.iloc[0])/(closing_data.iloc[0])
# Evaluating Log Returns
log_returns = np.log((closing_data.iloc[-1])/(closing_data.iloc[0]))
```
### Sharpe Ratio
Here I queried the closing data from the dataframe and used the ```.pct_change()``` function which calculates the percentage differnce from each day and the dropped all null values. This is neccessary since the first day has no percent change because there is no entry before it.

<img width="625" height="245" alt="Screenshot 2026-04-22 at 11 14 04 PM" src="https://github.com/user-attachments/assets/95dd9e25-352b-4fe3-8e01-bcf7a15ea853" />

- Return of Portfolio = **`annualized_returns`**
- Standard Deviation of the Portfolio's Excess Return = **`annualized volatility`**

- **`annualized_returns`** -> returns of a investment computed yearly for better comparison. (Mean of daily returns multiplied by number of trading days in a year)
- **`risk free rate`** -> theoretical rate of return on an investment with zero risk.
- **`annualized volatility`** -> the variance of an invesments returns computed yearly for better comparison. (Standard Deviation of Returns mulitplied by sqrt of number of trading days in a year)
```
# If annualized_velocity is 0 then sharpe_ratio will error so we create an edge case to prevent that
if annualized_volatility != 0:
   sharpe_ratio = (annualized_returns - risk_free_rate)  / annualized_volatility
else:
   sharp_ratio = np.nan
```
#### Annualized Returns
The formula for Annualized Returns is ```daily_mean_returns``` * ```trading_days_in_year```
```
# There are 252 trading days in a year
trading_days_in_year = 252
# Mean Returns
daily_mean_returns = daily_returns.mean()
# Annualized Returns
annualized_returns = daily_mean_returns * trading_days_in_year
```
#### Annualized Volatility
The formula for Annualized Volatility is ```daily_std_returns``` * ```np.sqrt(trading_days_in_year)``` 
Why Square Root? Because standard deviation is just the square root of variance so to annualize it you have to square root the number of trading days in a year as well.
```
# Standard Deviation Returns
daily_std_returns = daily_returns.std()
# Annualized Volatility
annualized_volatility = daily_std_returns*np.sqrt(trading_days_in_year)
```

### Rolling Sharpe Ratio
Utilizing the ```.rolling()``` method, we can calculate the rolling sharpe ratio by finding the "rolling" version of every variable in the sharpe ratio formula and plugging it in.
```
rolling_mean = daily_returns.rolling(window).mean()
rolling_std = daily_returns.rolling(window).std()
rolling_returns = rolling_mean * trading_days_in_year
rolling_volatility = rolling_std * np.sqrt(trading_days_in_year)
rolling_sharpe_ratio = ((rolling_returns - risk_free_rate) / (rolling_volatility)).dropna()
rolling_sharpe_ratio.plot()
```
### Results
Here I created a new dataframe that shows simple returns, log returns and the sharpe ratio of all tickers.
```
# Extracting Closing Data
results = pd.DataFrame((simple_returns, log_returns, sharpe_ratio), index = pd.Index(['Simple Returns','Log_Returns', 'Sharpe Ratio'], name = 'Results'))
# Example
Sharpe(['AAPL', 'SPY'], '2022-01-01', '2026-01-01')
```
<img width="1056" height="804" alt="Screenshot 2026-04-23 at 12 57 31 AM" src="https://github.com/user-attachments/assets/9c96c2c5-8047-4794-a8f5-4893ce2c9d31" />
