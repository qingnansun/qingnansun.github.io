---
title: 使用python构建ARIMA模型进行预测分析的小说明-forecast函数
date: 2018-04-26
tags: [python,ARIMA,预测,forecast函数]
updated: 
categories: 
permalink: 
keywords: [python,ARIMA,预测,forecast函数,qingnan,qingnansun,samboy]
description: Autoregressive Integrated Moving Average model(ARIMA)，即差分整合移动平均自回归模型，或称为整合移动平均自回归模型，是一种时间序列预测分析方法。今天我在实践过程中遇到一个小问题，后来看了官方文档才弄清楚，这里和大家分享一下。
toc: true    # table of content
top: false
comments: true  
---

&emsp;&emsp;Autoregressive Integrated Moving Average model(ARIMA)，即差分整合移动平均自回归模型，或称为整合移动平均自回归模型，是一种时间序列预测分析方法。今天我在实践过程中遇到一个小问题，后来看了官方文档才弄清楚，这里和大家分享一下。

&emsp;&emsp;首先分享三篇我觉得比较好并且容易上手的教程，其中包含源代码可以直接使用。第一篇是一个最简单的入门，是单步预测；第二篇可以进行多步预测；第三篇对于算法使用前的数据处理和分析进行了详细的介绍；第四篇也有相详尽的步骤和代码，并对数据进行了详细的分析，第五篇详细的介绍了从线性回归到AR、ARMA、ARIMA及GARCH等方法。

[How to Create an ARIMA Model for Time Series Forecasting with Python](https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/)
[How to Make Out-of-Sample Forecasts with ARIMA in Python](https://machinelearningmastery.com/make-sample-forecasts-arima-python/)
[Forecast a time series with ARIMA in Python](https://datascience.ibm.com/exchange/public/entry/view/815137c868b916821dec777bdc23013c)
[A Guide to Time Series Forecasting with ARIMA in Python 3](https://www.digitalocean.com/community/tutorials/a-guide-to-time-series-forecasting-with-arima-in-python-3)
[Time Series Analysis (TSA) in Python – Linear Models to GARCH](http://www.blackarbs.com/blog/time-series-analysis-in-python-linear-models-to-garch/11/1/2016)

&emsp;&emsp;以第二个链接中的代码为例。这个链接中的《5\. Multi-Step Out-of-Sample Forecast》将的是对样本量之外的多步预测，使用的Forecast function。具体的说，目前的数据为截止到12月24日的历年最低气温，现在要预测从12月25日到12月31日的最低气温。这里使用的代码为：

```
forecast = model_fit.forecast(steps=7)[0]
```

&emsp;&emsp;其中steps=7很好理解，就是预测未来七天的意思。可是后边方括号里的0让我很费解，而且把forecast的数据打印出来也很奇怪，是两行7个元素的数组，加一个二维的矩阵。后来看了官方文档之后，发现取0行是因为只有这一行才是预测的结果，第二行是预测的标准差（standard error），后边的二维矩阵是预测的置信区间。具体的官方解释如下：

```
ARIMAResults.forecast(steps=1, exog=None, alpha=0.05) 
```

Out-of-sample forecasts

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col class="field-name" style="box-sizing: border-box; margin: 0px; padding: 0px;"><col class="field-body" style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| Parameters: | 

**steps** : int
The number of out of sample forecasts from the end of the sample.

**exog** : array
If the model is an ARIMAX, you must provide out of sample values for the exogenous variables. This should not include the constant.

**alpha** : float
The confidence intervals for the forecasts are (1 – alpha) %

| Returns: | 

**forecast** : array
Array of out of sample forecasts

**stderr** : array
Array of the standard error of the forecasts.

**conf_int** : array
2d array of the confidence interval for the forecast

Notes：
Prediction is done in the levels of the original endogenous variable. If you would like prediction of differences in levels use <cite style="box-sizing: border-box; margin: 0px; padding: 0px;">predict</cite>

引用资料：[statsmodels.tsa.arima_model.ARIMAResults.forecast](http://www.statsmodels.org/devel/generated/statsmodels.tsa.arima_model.ARIMAResults.forecast.html)

***
本篇文章原发表于我的个人博客: [qingnansun.com](http://qingnansun.com/python_arima_forecast/)
