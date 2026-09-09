## Time Series Analysis

### Learning Objectives
By the end of this lesson, students will be able to:
1. Describe what a time series is
2. Decompose a time series into trend and seasonality
3. Compute the rate of return for a stock dataset

### What is a Time Series?
Time series: series of data points listed in time order
Example: Temperature during the day, number of taxi rides during a week, stock market price and ...
Trend: Long term progression (for example increase or decrease)
Seasonality: Patterns due to seasonal factors

## Review: Sort the following data frame based on date
```python
import pandas as pd
df = pd.DataFrame({'Value':['100','78','129'] , 'Date':['02/20/2015','01/15/2016','08/21/2015']})
```

## Activity: Obtain the trend and seasonality for air passenger dataset
Additive model: $x(t) = trend(t) + seasonality(t) + residual(t)$
Steps:
1- Plot the number of passenger based on Month: Hint:
```python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('Datasets/AirPassengers.csv')
df['Month'] = pd.to_datetime(df['Month'])
plt.plot(df['Month'], df['#Passengers'])
plt.show()
```
2- Set the index of data frame by Month:
`df  = df.set_index(['Month'])`
3- Apply the decomposition to data-frame -> Give us trend and seasonality
`import statsmodels.api as sm`
`decomposition = sm.tsa.seasonal_decompose(df, model='additive')`
4- Plot trend, seasonality and residual for passenger dataset

```python
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm

# Load and plot passaenger time series
df = pd.read_csv('Datasets/AirPassengers.csv')
df['Month'] = pd.to_datetime(df['Month'])
plt.plot(df['Month'], df['#Passengers'])
plt.show()

# Apply decompostion analysis to the time series
df  = df.set_index(['Month'])
decomposition = sm.tsa.seasonal_decompose(df, model='additive')
decomposition.plot()
plt.show()
```
## Sampling and Smoothing
Most of the time, for time series analysis, the data has many jumps and downs.
It is desired to have smoother version of time series.
We have two options:
1- Sampling the time series
2- Smoothing the time series

## Activity: Time Series Sampling and Smoothing on Apple dataset
Task: Plot the "Close", which is stock market price at closing time (5:30 p.m. NY time), its sampled version and its smoothed version.
Steps:
1- Load and plot Apple Stock Market dataset:
Hint:
```python
import pandas as pd
data = pd.read_csv('Datasets/AAPL.csv')
data['Date'] = pd.to_datetime(data['Date'])
data['Tick'] = range(0, len(data))
plt.plot(data['Date'], data['Close'])
plt.show()
```
2- Sample this dataset and plot it:
Hint: use `data.sample()`
3- Smooth this time series ("Close"):
Hint: use `data['Close'].rolling(window=5).mean()`

```python
data = pd.read_csv('Datasets/AAPL.csv')
data['Date'] = pd.to_datetime(data['Date'])
data['Tick'] = range(0, len(data))
plt.plot(data['Date'], data['Close'], label='Original')

# Sample time series
data_one_tenth = data.sample(frac=0.5)
data_one_tenth = data_one_tenth.sort_values(by=['Tick'])
plt.plot(data_one_tenth['Date'], data_one_tenth['Close'], label='Sampled')

# Smooth the dataset

data['Rolling_Mean']  = data['Close'].rolling(window=5).mean()
plt.plot(data['Date'], data['Rolling_Mean'], label='Smooth')

# plot them all
plt.legend()
plt.show()
```
## Computing Rate of Return

In order to compute the return for a specific period, we slice the dataset to that date range and compare prices at the start and end of it.

Task: compute the rate of return for Apple stock for March 2017 using the local `AAPL.csv` (no external API or account needed)
1- First read this article: [Rate of Return, Mean, and Variance](https://www.quantconnect.com/tutorials/introduction-to-financial-python/rate-of-return,-mean-and-variance)
2- Translate the formula to Python code

```python
import pandas as pd
import numpy as np

data = pd.read_csv('Datasets/AAPL.csv')
data['Date'] = pd.to_datetime(data['Date'])

march_2017 = data[(data['Date'] >= '2017-03-01') & (data['Date'] < '2017-04-01')]

# Compound rate of return, via log prices
march_2017 = march_2017.copy()
march_2017['log_price'] = np.log(march_2017['Close'])
x = np.diff(march_2017['log_price'])
print(x.sum() * 100)

# Simpler way: percent change from first to last close in the period
returns = march_2017['Close'].pct_change()
print(returns.sum() * 100)
```

## Topics
- What is a time series; trend and seasonality
- Decomposing a time series (`statsmodels.tsa.seasonal_decompose`)
- Sampling and smoothing (rolling mean)
- Rate of return

## Resources
- Watch these series of videos blog [Python Programming for Finance](https://pythonprogramming.net/getting-stock-prices-python-programming-for-finance/)

## Challenges

Deliverable: a notebook with the decomposition plot, the sampling/smoothing plot, and the March 2017 return calculation from this lesson, plus the extension below.

1. Complete the trend/seasonality decomposition activity on `AirPassengers.csv`
2. Complete the sampling and smoothing activity on `AAPL.csv`
3. Complete the March 2017 rate-of-return activity above
4. Extension: pick a different month in `AAPL.csv` (check the date range in the file first) and compute its rate of return. Was it a better or worse month than March 2017?

## Rubric
| Criteria | Meets expectations |
|---|---|
| Decomposition | Trend, seasonality, and residual plotted and correctly labeled |
| Sampling/smoothing | Original, sampled, and smoothed series all plotted together with a legend |
| Rate of return | March 2017 return computed correctly with both methods, and they roughly agree |
| Extension | A second month's return computed and compared to March 2017 |

### Bonus
The [Time Series Challenges notebook](../Notebooks/Challenges_Time%20Series.ipynb) has extra practice: date-based slicing (by year, by month, by custom range), plus a synthetic user-comments dataset (`Datasets/user_comments.csv`) for practicing `.str.contains()` and datetime filtering on a non-financial time series.
