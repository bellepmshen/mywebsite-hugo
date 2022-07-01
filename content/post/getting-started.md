---
title: Build a Time-Series ARIMA Model for Stock Market Forecast in Python
description: Getting started with personal-web
date: "2022-07-01T09:37:55+02:00"
publishDate: "2022-07-01T09:37:55+02:00"
---

In this articel, ARIMA algorithm will be introduced and we will talk about how to build a time-series ARIMA model in Python to make real-time forecast for stock market.

<!--more-->
<br>
Here is the content in this article:

### Content:<br/>
<br>
- What is ARIMA?<br>
- Stock Market Forecast Codes in Python<br>

### What is ARIMA?<br>

ARIMA stands for <font><i>"Autoregressive Integrated Moving Average"</i></font> and it is an algorithm for forecasting time-series data, such as predicting stock market price, or forecasting daily temperature.<br>

ARIMA is composed of three parts:<br>

**I. AR (Autoregression):** <br>
<br>
	- It is a linear combination of lagged dependent variables i.e., observations <br>
	- Parameter Notation: <font><i>"p"</i></font>, the number of lag orders <br>
	- Formula:

            {{< figure src="/post/images/AR_formula.png">}}

**II. MA (Moving Average):**<br>
<br>
	- It is a linear combination of lagged error terms between actual and forecast values<br>
	- Parameter Notation: <font><i>"q"</i></font>, the number of lagged forecast errors<br>
	- Formula:<br>

            {{< figure src="/post/images/MA_formula.png">}}

**III. I (Integrated):**<br>
<br>
	- The differences between original observations and lagged ones to make the time series data stationary.<br>
	- Parameter Notation: <font><i>"d"</i></font>, the number of difference levels <br>
	- Formula (take the 1st difference level as an example, i.e., d = 1):<br>

            {{< figure src="/post/images/integrated_formula.png">}}


### Stock Market Forecast Codes in Python:<br>

In this session, we take Facebook/Meta data via yfinace API to build an ARIMA model to forecast the next minute stock price.<br>

Here is the process flow of codes:

        {{< figure src="/post/images/process_flow.png">}}

**I. Import libraries:**<br>

```py
import datetime as dt
from time_series import Time_Series
```
<br>
The datetime library will let us obtain the duration of time from retrieving data to forecast the next minute stock price.<br>

The time_series module contains the functions we need for making the prediction on stock market price.<br>

<br>

**II. Instantiate the class and get 7-day stock price:**<br>

```py
ts = Time_Series()
stock = ts.get_data('meta')
```
<br>
By using yfinance API, we can obtain 7-day of stock data by minute.<br>

<br>

**III. Train & Test Split:**<br>

```py
train, test = ts.split()
```
<br>
In a time-series problem, the data are in sequence, which means we will not split the data into train and test randomly, so here we take the last 50 observations as our test data due to computer power constraint.<br>

<br>

**IV. Log transform:**<br>

```py
train_1, test_1 = ts.make_log()
```
<br>
We take natural logarithm (log(1+x)) to flatten the fluctuation.<br>

<br>

**V. Get (p, d, q) permutation:**<br>

```py
params = ts.generate_params()
```
<br>
We generate different combinations of (p, d, q) for hyperparameters tuning to find out the smallest RMSE (Root Mean Square Errors).<br>

<br>

**VI. Hyperparameters Tuning:**<br>

```py
rmse_box, best_pdq = ts.rmse_calculation()
```
<br>
How to train a time-series model?<br>
<br>
When building a time-series model, we get a forecast for the next timestamp based on the data from the previous timestamps which means, your train data size will gradually increase for each iterations (see the detail codes in the GitHub link below) cause we want to forecast the "next timestamp." <br>

For example, your last timestamp of train data is "2022-06-27 15:56:00", and you build a model from the train data, so you get a forecast for "2022-06-27 15:57:00."  What if we want to see the forecast of "2022-06-27 15:58:00"?
Then, you will add the acutal observation of "2022-06-27 15:57:00" to train data, and this timestamp will be your last observation in the train data.  You'll build a model from this "new" train data, and get a forecast for the next minute which is "2022-06-27 15:58:00."<br>

Here we use the "forecast()" function from ARIMA to get "out-of-sample" forecast.<br>

Thus, the code above performs hyperparameters tunings to iterate different permutations of (p, d, q) and to see which permutation yields the smallest RMSE.<br>

<br>

**VII. Build final model:**<br>

```python
ts.final_training()
```
<br>
We train the whole 7-day data with the best (p, d, q) permutation we obtain from hyperparameters tuning job to get a forecast for the next minute (refer to the picture below)!

        {{< figure src="/post/images/forecast_result.png">}}

Below are the full codes:<br>

```py
def execute():

"""This function is to execute all the functions to get 
the next minute open price.

Returns

-------

str

a message to show the next minute open price

"""

try:
# create the beginning timestamp for calculating 
# the runtime
t1 = dt.datetime.now()

# instantiate the class
ts = Time_Series()

# get the 7-day of stock data by minute
stock = ts.get_data('meta')

# train and test split
train, test = ts.split()

# take log on both of train & test data to flatten 
#the fluctuation
train_1, test_1 = ts.make_log()

# generate the p, d, q permutation
params = ts.generate_params()

# hyperparameters tuning to get the smallest RMSE 
# with corresponding p, d, q
rmse_box, best_pdq = ts.rmse_calculation()

# train the whole data with the best p, d, q obtained 
# from hyperparameters tuning and show the next minute 
# forecast
print(ts.final_training())

# get the timestamp to obtain the timedelta of runtime
t2 = dt.datetime.now()

# get the runtime
return f"total processing time: {(t2-t1).seconds} seconds"

except Exception as err:

print(err)

  
# execute the function
execute()
```
<br>

<font color = "blue"><b>Full codes can be found
<a href="https://github.com/bellepmshen/time_series_real_time_forecast">here!</a><br></b></font>

### References: 

<pre>
- <a href="https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/">https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/</a>
- <a href="https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/#:~:text=ARIMA%20is%20an%20acronym%20that,structures%20in%20time%20series%20data.">https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python#:~:text=ARIMA%20is%20an%20acronym%20that,structures%20in%20time%20series%20data.</a>
- <a href="https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average">https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average</a>
- <a href="https://faculty.fuqua.duke.edu/~rnau/Decision411_2007/411arim.htm">https://faculty.fuqua.duke.edu/~rnau/Decision411_2007/411arim.htm</a>
- <a href="https://online.stat.psu.edu/stat510/book/export/html/665">https://online.stat.psu.edu/stat510/book/export/html/665</a>
</pre>


