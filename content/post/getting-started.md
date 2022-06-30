---
title: Build a Time-Series ARIMA Model for Stock Market Forecast in Python
description: Getting started with personal-web
date: "2022-06-30T09:37:55+02:00"
publishDate: "2022-06-30T09:37:55+02:00"
---

Here is the content in this article:

### Content:<br>

- What is ARIMA?<br>
- Stock Market Forecast Codes in Python<br>

### What is ARIMA?<br>

ARIMA stands for <font><i>"Autoregressive Integrated Moving Average"</i></font> and it is an algorithm for forecasting time-series data, such as predicting stock market price, or forecasting daily temperature.<br>

ARIMA is composed of three parts:<br>

I. AR (Autoregression): <br>
	- It is a linear combination of lagged dependent variables i.e., observations
	- Parameter Notation: <font><i>"p"</i></font>, the number of lag orders
	- Formula:
    	$
		\begin {align}
		Y_t\;
		&=\;
		\beta\;+\;
		\alpha_1 Y_{t-1}\;+\;
		\alpha_2 Y_{t-2}\;+\;
		...+\;
		\alpha_p Y_{t-p}\;\\\\
		&= \beta\;+\;
		\sum_{i=1}^{p} \alpha_{i}Y_{t-i}\;
		\end {align}
	    $
    


