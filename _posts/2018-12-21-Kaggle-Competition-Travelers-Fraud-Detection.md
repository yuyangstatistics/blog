---
title: Kaggle Competition--Travelers Fraud Detection
date: 2018-12-21 12:28:12 -0500
categories: [Data_Science]
tags: [kaggle]
---

This blog is about what our group has done in the [Kaggle competition for Travelers Fraud Detection](https://www.kaggle.com/c/2018-trv-statistical-modeling-competition-umn) and what I have learnt through this experience. Hope this would help you get some ideas when doing similar projects.

The whole material could be found on [My Github](https://github.com/yuyangstatistics/projects/tree/main/Kaggle_Travelers). Programming stress should be put on [Data Cleaning](https://github.com/yuyangstatistics/projects/blob/main/Kaggle_Travelers/notebooks/data_cleaning.ipynb), [XGBoost](https://github.com/yuyangstatistics/projects/blob/main/Kaggle_Travelers/notebooks/XGBoost.ipynb), [LightGBM](https://github.com/yuyangstatistics/projects/blob/main/Kaggle_Travelers/notebooks/LightGBM.ipynb), [Model Comparison](https://github.com/yuyangstatistics/projects/blob/main/Kaggle_Travelers/notebooks/Model_comparison.ipynb), and [Classification](https://github.com/yuyangstatistics/projects/blob/main/Kaggle_Travelers/notebooks/Classification.ipynb). The detailed coding could be found on these notebooks. Credit goes to the whole team: King Yiu Suen, Sam Piehl, Somyi Baek, Xun xian, and Yu Yang.

From this project, I learned several new things.

1. When tuning the parameters of XGBoost model, don't try to use grid search to find the optimal parameters with one single run. Instead, tune the parameters one by one. I found this [Reference](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/) to be a useful guide.

2. It is a good habit to clean the data thoroughly. In our project, we generated several cleaned dataset and the cleaning extents are different, which then requires us to do further cleaning inside the model notebooks. Therefore, if you are going to organize a similar project, my suggestion is to well organize the datasets to avoid time wasting in the later stage.

3. The idea of *Cross Validataion* should be used through out the project. It is a vital tool to avoid overfitting.

4. When coping with the LightGBM model, we found that sometimes fewer features might give better results. This reminds us that including as many as possible features may not be a good thing. The bad performance might be due to the correlation, which requires further investigation. Therefore, it might worth a try to delete some features when trying to find the best feature combination.

5. A question is raised: should Bayesian tuning be used in similar cases? According to the results of our tests, Bayesian tunning cannot beat manual tuning in XGBoost and LightGBM. The effectiveness of Bayesian tunning needs to be furthered considered.

6. Logistic regression and random forest don't perform well in such a case, just as suggested by many Kaggle competitions. So, when doing classification, we might ignore such methods and put our time and focus on XGBoost, LightGBM, Catboost and etc.

7. Several things need to be studied: Stacking, WOE. Future notes regarding these will be added soon.


