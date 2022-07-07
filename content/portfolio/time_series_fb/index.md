---
title: Facebook/Meta Stock Price Forecasting
description: This is the description of our sample project
date: "2022-06-10T19:47:09+02:00"
jobDate: 2022
work: [Time Series, Forecast, Stock Price]
techs: [ARIMA, Augmented Dickey-Fuller test, statsmodels]
# designs: [Photoshop]
thumbnail: loan-credit/stock.jpeg
projectUrl: https://github.com/bellepmshen/time_series_FB_stock
# testimonial:
#   name: John Doe
#   role: CEO @Example
#   image: loan-credit/loan-1.jpeg
#   text: Prow scuttle parrel provost Sail ho shrouds spirits boom mizzenmast yardarm. Pinnace holystone mizzenmast quarter crow's nest nipperkin
---

<!-- This would be a description of your sample project. You can add any content you'd like. -->

<font><b><u>Project Goal</b></u></font><br>
The goal of this project was to build an ARIMA (autoregressive integrated moving average) model to forecast by using the stock open price of FB on Aug. 31, 2021 and the model was trained by using the price from Aug 1 to 30, 2021.<br> 

<font><b><u>Library</b></u></font><br>
We used Pandas for data analysis, matplotlib for visualization, NumPy & scikit-learn for model evaluation, and statsmodels for the ARIMA algorithm and Augmented Dickey-Fuller test.

<font><b><u>ARIMA Model Requirements</b></u></font><br>
In this ARIMA model, the order of (P, D, Q) values should be decided and P represents autoregressive terms, D is the number of difference levels in order to get stationary data and Q stands for moving-average terms.<br>

For selecting these values, plotting partial autocorrelation function (pacf) & autocorrelation function (acf) can get the reference values of P and Q respectively by taking the cut-off point.<br>

By performing Augmented Dickey-Fuller test to obtain p-value, we can obtain what would be a good value of D with p-value < 0.05 which means the data was stationary.<br>

<font><b><u>Data Analysis Result</b></u></font><br>
By plotting pacf and acf, the value of "2" might be a good value for P, but we really could not see what a good value for Q might be.<br>

And one difference level of the data would allow us to get a p-value smaller than 0.05 by running the Augmented Dickey-Fuller test.<br> 

<font><b><u>Hyperparameters Tuning</b></u></font><br>
Overall, those P, D, Q values we had from the above data analysis results only act as a reference. We still needed to get the optimized P, D, Q values from doing hyperparameter tuning, and to see which permutations of P, D, Q yields the smallest RMSE (Root Mean Square Error).

p.s.: Because this was similar to a regression problem, thus RMSE would be a better metric to evaluate the model.<br>

<font><b><u>Results</b></u></font><br>
From the hyperparameter tuning results, the best permutation of P, D, Q was obtained, so we would use this order to train the whole dataset getting the final ARIMA model for forecasting the next day stock price.<br>
Resulting in an RMSE = $0.88 for the price on Aug. 31.<br>

For detail codes and graphs, please check the GitHub link above :point_up_2:<br>

Want to get the next minute forecast? download my notebook <font color = "334AFF"><a href = "https://github.com/bellepmshen/time_series_FB_stock/blob/main/forecast.ipynb"><u>here</u></a></font> and run it by yourself!<br>

<font><b><u>Real-Time Forecasting</b></u></font><br>

If you want to forecast other companies stock market price in real time, try my notebook 
<font color = "334AFF"><a href = "https://github.com/bellepmshen/time_series_real_time_forecast"><u>here.</u></a></font><br>

And I have an article which explains how my codes work, you can check my <font color = "334AFF"><a href = "https://bellepmshen.github.io/post/time_series_arima/"><u>post.</u></a></font><br>

<font size = "-3"><i>photo credit: https://www.financialexpress.com/investing-abroad/featured-stories/us-stock-futures-fall-as-big-week-of-earnings-reports-kicks-off/2495305/</i></font>