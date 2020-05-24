---
title: MinneMUDAC 2019 Student Data Science Challenge
date: 2020-01-03 12:28:12 -0500
img: minnemudac.png
comments: true
categories: [Data_Science, MinneMUDAC]
tags: [project]
---
MinneMUDAC 2019 Student Data Challenge is organized by MinneAnalytics every year. There are several divisions: novice division, undergradutate division, and graduate division. For 2019, the problem is to predict the price of soybean future contracts in the volatile market for one week. 

Among 24 graduate teams, we ranked 2nd and won Analytic Acumen Award. Our work was greatly appreciated by the judges and people in the industry. And we have been invited to give talks in companies and organizations. This blog is to share part of our work, and hope it might be helpful. Check [my github](https://github.com/yuyangstatistics/projects/tree/master/MinneMUDAC) for more detail about this project.

This blog will not talk in detail about the results of our model, but will focus more on the methods and whole modeling pipeline. The framework is as follow:
- Introduction to the project
- Our work
- My role
- Lessons learnt from this project
- What would have been done differently given the 2nd chance?

## Introduction to the project
The objective of this project is to investigate the factors that influence the soybean futures closing prices and predict soybean closing prices for 5 days: November 4-8th, and for 3 contract months: March, May, and July 2020.

## Our Work
Credit goes to the whole team: **Somyi Baek, Cora Crown, Sarah Milstein, Yu Yang**.

### Data Pipeline
Data is the most critical part in our project. Large portion of time was spent on collecting and processing data. There are three stages: data gathering, feature engineering, and stationarizing & scaling.


#### Data Gathering

We got the opportunity to talk to previous and current Cargill employees and obtained some understandings on the futures market and economic patterns. Based on their advice, we started collecting data.

We directly downloaded the datasets that were available with clean format. And for commodity price data, clean format was not available, and hence we crawled it from [MRCI's Free Historical Futures Prices](https://www.mrci.com/ohlc/). Check the [notebook](https://github.com/yuyangstatistics/projects/blob/master/MinneMUDAC/notebooks/spider.ipynb) for more detail.

Commodity prices intertwine with each other, so we collected historical commodity prices data, including soybean, corn, canola, soybean meal, soybean oil, rice, and hog, from 2015 to 2019. Also, to incorporate the effect of external features, we collected weather data and file records, macroeconomic indicators, such as interest rate and Dow Jones indices. Stock market is closely related to the political events, so we collected tweets and tariff data. Besides, the usage information of soybean is obtained, including planting, meal, and stocks. Tweets data is obtained from http://www.trumptwitterarchive.com/archive.

#### Feature Engineering

*Incorporate weekend data*: one special property of stock price is that data is only available on weekdays during business hours. In the meanwhile, external data sources, such as weather and tweets, are also available in weekends and during off-busineess hours, and these data would affect the price in the next day or next week. In order to utilize this part of information, we use the average of Saturday, Sunday, and Monday to be the data on Monday. And for tweets posted after market hours, we integrate it to the next day.

*Shift old contracts*: for contracts in the previous years, the dates don't match, so we shifted the old contracts data to align with the year 2019.

*Sentiment analysis of tweets*: use LDC topic modeling to cluster tweets. Select trade and economy relevant tweets, and then do sentiment analysis. Check the code and result in [tweet.ipynb](https://github.com/yuyangstatistics/projects/blob/master/MinneMUDAC/notebooks/tweet.ipynb) and [tweetLDA11.html](https://github.com/yuyangstatistics/projects/blob/master/MinneMUDAC/notebooks/tweetLDA11.html).

#### Stationarizing & Scaling

Since we are dealing with time series data, we need to pay attention to the stationarity of the time series. ADF test and KPSS test were done to validate data stationarizing. After that, we calculate 1-order difference to stationarize the data and do scaling for all features.

### Data Exploration 

Check [our slides](https://github.com/yuyangstatistics/projects/tree/master/MinneMUDAC/talks) for more detail about the results.

### Modeling
We observe that for commodities except soybean and corn, the length of the contract price data is much shorter. Our strategy is to consider two modeling ideas, external models and commodity models. External models make use of external features, corn, and soybean data, while commodity models make use of short-term commodity data. After that, model selection and averaging is done to get the final model. 

For external models, we consider linear regression, ridge, lasso, XGBoost, and LSTM. And for commodity models, VAR(vector autoregression) and ARMAX(ARMA with external features) are considered.

### Model Interpretation

[SHAP](https://github.com/slundberg/shap) has been shown to be a consistent and theoretically sound way to evaluate features' attribution, and its graphical representation is clear and informative. Hence, we use it for interpreting models.

## My role

We discuss together for all of the modeling and data wrangling ideas, and do coding seperately. In the data part, I am responsible for collecting tariff data, crawling the data, and analyzing tweets data. In the modeling part, I work on linear regression model, ridge regression, Lasso, and XGBoost.

## Lessons learnt from this project

- Data is the key. Ask specialist for domain knowledge and try to collect as much relevant data as possible.
- Keeping a clear record of the version of data would help with data wrangling. 
- When crawling the data, note that some websites may have tiny mistakes and should write code to allow these errors.
- Modeling requires teamwork. By discussing, we can see our mistakes easier and get more ideas.


## What we did well in this project?

- Collaboration. It is the good collaboration in us that leads to the success of our project. We come up with ideas together and check the plausibility and possible mistakes. We trust each other. We do coding seperately and integrate our result in an organized way.
- Data gathering and processing. We consulted specialists for domain knowledge and collected data from many sources. And we took many factors into consideration when processing the data, such as stationarity and weekend property.
- Model interpretation. Our models don't just give the final prediction results, but also provide interpretation, which makes the machine learning models not a black box any more.
- Slides. Our slides and talks are organized in a clear and logical way.

## What would have been done differently given the 2nd chance?
- Fine tune XGBoost model parameters.
- Using the last available week as validation to determine model averaging weight may not be appropriate. 
- Time management. 

