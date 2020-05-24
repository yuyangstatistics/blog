---
title: ISLR Review
date: 2018-08-12 12:28:12 -0500
img: ISLR.jpg
comments: true
categories: [Statistics]
tags: [statistical-learning]
---

* [3 Linear Regression](#3)
    - [3.0 Introduction](#3.0)
    - [3.1 Simple Linear Regression](#3.1)
    - [3.2 Multiple Linear Regression](#3.2)
    - [3.3 Other Considerations in the Regression Model](#3.3)
    - [3.4 The Marketing Plan](#3.4)
    - [3.5 Comparison of Linear Regression with K-Nearest Neighbors](#3.5)
* [4 Classification](#4)
    - [4.0 Introduction](#4.0)
    - [4.1 An Overview of Classification](#4.1)
    - [4.2 Why Not Linear Regression?](#4.2)
    - [4.3 Logistic Regression](#4.3)
    - [4.4 Linear Discriminant Analysis](#4.4)
    - [4.5 A Comparison of Classfication Methods](#4.5)
* [5 Resampling Methods](#5)
    - [5.0 Introduction](#5.0)
    - [5.1 Cross-Validation](#5.1)
    - [5.2 The Bootstrap](#5.2)
* [6 Linear Model Selection and Regularization](#6)
    - [6.0 Introduction](#6.0)
    - [6.1 Subset Selection](#6.1)
    - [6.2 Shrinkage Methods](#6.2)
    - [6.3 Dimension Reduction Methods](#6.3)
    - [6.4 Considerations in High Dimensions](#6.4)
* [7 Moving Beyond Linearity](#7)
    - [7.0 Introduction](#7.0)
    - [7.1 Polynomial Regression](#7.1)
    - [7.2 Step Functions](#7.2)
    - [7.3 Basis Functios](#7.3)
    - [7.4 Regression Splines](#7.4)
    - [7.5 Smoothing Splines](#7.5)
    - [7.6 Local Regression](#7.6)
    - [7.7 Generalized Additive Models](#7.7)
* [8 Tree-Based Methods](#8)
    - [8.0 Introduction](#8.0)
    - [8.1 The Basics of Decision Trees](#8.1)
    - [8.2 Bagging, Random Forests, Boosting](#8.2)
* [9 Support Vector Machines](#9)
    - [9.0 Introduction](#9.0)
    - [9.1 Maximal Margin Classifier](#9.1)
    - [9.2 Support Vector Classfiers](#9.2)
    - [9.3 Support Vector Machines](#9.3)
    - [9.4 SVMs with More than Two Classes](#9.4)
    - [9.5 Relationship to Logistic Regression](#9.5)
* [10 Unsupervised Learning](#10)
    - [10.0 Introduction](#10.0)
    - [10.1 The Challenge of Unsupervised Learning](#10.1)
    - [10.2 Principal Components Analysis](#10.2)
    - [10.3 Clustering Methods](#10.3)


<h2 id="3">3 Linear Regression</h2>

<h3 id="3.0">3.0 Introduction</h3>
<h3 id="3.1">3.1 Simple Linear Regression</h3>
<h3 id="3.2">3.2 Multiple Linear Regression</h3>
<h3 id="3.3">3.3 Other Considerations in the Regression Model</h3>
<h3 id="3.4">3.4 The Marketing Plan</h3>
<h3 id="3.5">3.5 Comparison of Linear Regression with K-Nearest Neighbors</h3>


<h2 id="4">4 Classification</h2>

<h3 id="4.0">4.0 Introduction</h3>
<h3 id="4.1">4.1 An Overview of Classification</h3>
<h3 id="4.2">4.2 Why Not Linear Regression?</h3>
<h3 id="4.3">4.3 Logistic Regression</h3>
<h3 id="4.4">4.4 Linear Discriminant Analysis</h3>
<h3 id="4.5">4.5 A Comparison of Classfication Methods</h3>


<h2 id="5">5 Resampling Methods</h2>

<h3 id="5.0">5.0 Introduction</h3>
<h3 id="5.1">5.1 Cross-Validation</h3>
<h3 id="5.2">5.2 The Bootstrap</h3>


<h2 id="6">6 Linear Model Selection and Regularization</h2>

<h3 id="6.0">6.0 Introduction</h3>

1. Why would we use alternative fitting procedures instead of least squares?
    - _Prediction Accuracy_:
        + n >> _p_: low bias
        + _n_ not much larger than _p_: easily overfitting, high variance
        + _n_ smaller thatn _p_: least squares not feasible
        + alternative procedures could decrease variance with negligible increase in bias
    - _Model Interpretability_:
        + unnecessary variables lead to higher model complexity
        + feature selection could remove these variables_Subset Selection_

2. The difference between _Subset Selection_, _Shrinkage_, and _Dimension Reduction_?
    - _Subset Selection_: fit a model involving a subset of _p_ predictors; computationally inefficient
    - _Shrinkage_: fit a model involving all _p_ predictors; computationally speaking, almost the same as least squares
    - _Dimension Reduction_: fit a model involving _M_ projections of _p_ predictors

3. Is _Subset Selection_ equavalent to _feature selection_? Then what about _lasso_? 
    - No. _Subset Selection_ could do feature selection, _lasso_ could also do feature selection. But _Dimension Reduction_ is not a feature selection method.

<h3 id="6.1">6.1 Subset Selection</h3>

1. The pros and cons of _Best Subset Selection_, _Forward Stepwise Selection_, and _Backward Stepwise Selection_?
    - _Computationally_: _Best Subset Selection_ is more time-consuming.
    - _Backward Stepwise Selection_ is not feasible when n << p.

2. What is _Forward Stagewise Selection_'s essence? Is it similar to _Partial Least Squares_?

3. Two ways to estimate test error.
    - Adjust training error to account for the bias due to overfitting.(why not the variance due to overfitting)
    - Validation set approach and cross-validation approach.

4. The comparisons and ituitions of the four criteria.
    - BIC places heavier penalty on model complexity than C_p.
    - RSS could be replaced with _deviance_ for general cases.
    - RSS/(n-d-1) intuitively controls the involvement of unnecessary variables. Once all necessary variables have been included, adding extra features would increase the denominator while little decrese in the nominator.

5. Comparison between the two testing error estimation?
    - Validation and cross-validation make no assumption of the model, more general.

6. The point behind _one-standard-error rule_?
    - Parsimony

<h3 id="6.2">6.2 Shrinkage Methods</h3>

1. The idea of shrinkage?
    - shrink the coefficients to zero, and thus reduce the variance 

2. Standardization?
    - standardize before ridge regression(certainly, PCR as well)
    - PLS
    - lasso needs standardization too?

3. Ridge regression's pros?
    - _bias-variance-tradeoff_
    - works best when least squares estimates have high variance
    - for least squares, n > p: low bias, high variance; n < p: no unique solution. While ridge regression works in both situations.

4. Comparison between ridge regression and lasso?
    - none of the coefficients of ridge regression is exactly zero, which might lead to interpretability problem, while lasso would shrink some coefficients to exact zero and do feature selection.
    - Graphical intution of these two methods.
    ![contour: Ridge vs. Lasso]({{site.baseurl}}/assets/img/ridge_lasso_contour.jpg)
    - lasso performas better when the true model only depends on a small amount of predictors.
    - ridge regression shrinks all coefficients by the same proportion while lasso shrinks most of the coefficients by similar proportion and sufficiently small coefficients directly to zero. Recall the illustrating graph.
    ![coef: Ridge vs. Lasso]({{site.baseurl}}/assets/img/ridge_lasso_coef.jpg)
    - Bayesian interpretation: 
        + ridge regression <-> Gaussian prior, thus shrinked coefficients vary around zero
        + lasso <-> Laplace prior, thus shrinked some coefficients to exact zero
    ![Bayesian: Ridge vs. Lasso]({{site.baseurl}}/assets/img/ridge_lasso_bayes.jpg)

<h3 id="6.3">6.3 Dimension Reduction Methods</h3>

1. The idea of _Dimesion Reduction_?
    - constrain through the form of the coefficients

2. The idea of PCA?
    - first principle component shows the largest variability of predictors.
    - it summarizes the predictors.

3. The assumption of PCR?
    - assume that the directions which the predictors shows the most variation are the directions assocaited with the response.

4. PCR and ridge regression?
    - They are closely related. When the true model relies on a small set of the original features, PCR and ridge regression may not perform well.
    - ridge regression, continuous version of PCR. small lambda <-> large M

5. The idea of PLS?
    - **why call partial least squares? what's the connection with least squares?**
    - cons of PCR: The directions that best explain the predictors doesn't guarantee to best explain the response. So, PLS intends to use the response Y's information, a supervised version of PCR. 
    - **the interpretation of the new feature selection procedure, from the aspect of information?**

6. Does PLS negelct the information which reflects the most variation of predictors?
    - We can consider these two dimension reduction methods identifying new features from different aspect of viewing the problem. PCR identifies new features reflecting the most variation while PLS identifies new features that relates both X and Y most.

<h3 id="6.4">6.4 Considerations in High Dimensions</h3>

1. The problems of high dimensions
    - Regardless of whether or not there truly is relationship between response and predictors, in high dimensional case, least squares will yield the coefficients that make a perfect fitting, namely RSS=0, and thus overfitting.
    - Including additional variables leads to a vast increase in the variance of coefficient estimates.
    - Those four criteria to select models don't work here.
    - Multicollinearity is extreme. Thus we cannot identify which feature is truly predictive of the response. There are many different models reaching the same prediction.

2. What is the _curse of dimensionality_?
    - Adding signal features that are associated with the response will improve the fitted model while adding noise features that are not associated with the response will deteriorate the model, leading to high variance of the coefficient estimates.

3. Several points to notice in high dimension
    - Traditional measures of fitness could not be used to demonstrate the performance of high dimensional models. Use independent test set or cross-validation instead.
    - When we have got a model, we need to know that it is only one of the many possible models for prediction, and it requires further validation.(corresponding to the 4th problem of high dimensions.)



<h2 id="7">7 Moving Beyond Linearity</h2>

<h3 id="7.0">7.0 Introduction</h3>

Chapter 6 improves model by reducing model complexity and is still in the framework of linear assumption.



<h3 id="7.1">7.1 Polynomial Regression</h3>

1. The individual coefficients are not of particular interest, and the point is to understand the relationship.

<h3 id="7.2">7.2 Step Functions</h3>

1. Pros and cons of step functions?
    - pros: Polynomial Regression imposes a global structure on the non-linear function of X, while step functions do not.
    - cons: can easily miss the pattern of the relationship

2. The idea of step functions
    - Convert a continuous variable into an ordered categorical variable, K + 1 dummy variables.
    - can take it as piecewise-constant regression

3. The interpretation of the coefficients
    - beta_0
    - beta_i (i >= 1)

4. Why is step functions popular in biostatistics and epidemiology? Do these field have knowledge of the natural breakpoints?

<h3 id="7.3">7.3 Basis Functions</h3>

1. The relationship between _Basis Functions_ and _Polynomial Regression_ and _Step Functions_?

2. Note that it still use the linear regression framework.

<h3 id="7.4">7.4 Regression Splines</h3>

1. Definition of _knots_?

2. The difference between _piecewise polynomial regression_ and _regression splines_?
    - regression splines satisfies the constraints on continuity and derivative continuity.

3. How to understand _smooth_?
    - In Mathematics, a smooth function is infinitely differentiable. However, in computer science, only several level of differentiable is required.(Still not sure.)

4. The definition of a *degree_d spline*?

5. **Would continuity in derivatives at degree k automatically satisfies continuity at lower degree of derivatives?**

Despite of the performance at the boundaries, given the same degrees of freedom, is _Regression splines_ superior to _Polynomial Regression_? Would it be more stable in other ranges?

<h3 id="7.5">7.5 Smoothing Splines</h3>

<h3 id="7.6">7.6 Local Regression</h3>

<h3 id="7.7">7.7 Generalized Additive Models</h3>



<h2 id="8">8 Tree-Based Methods</h2>

<h3 id="8.0">8.0 Introduction</h3>
<h3 id="8.1">8.1 The Basics of Decision Trees</h3>
<h3 id="8.2">8.2 Bagging, Random Forests, Boosting</h3>


<h2 id="9">9 Support Vector Machines</h2>

<h3 id="9.0">9.0 Introduction</h3>
<h3 id="9.1">9.1 Maximal Margin Classifier</h3>
<h3 id="9.2">9.2 Support Vector Classfiers</h3>
<h3 id="9.3">9.3 Support Vector Machines</h3>
<h3 id="9.4">9.4 SVMs with More than Two Classes</h3>
<h3 id="9.5">9.5 Relationship to Logistic Regression</h3>


<h2 id="10">10 Unsupervised Learning</h2>
<h3 id="10.0">10.0 Introduction</h3>
<h3 id="10.1">10.1 The Challenge of Unsupervised Learning</h3>
<h3 id="10.2">10.2 Principal Components Analysis</h3>
<h3 id="10.3">10.3 Clustering Methods</h3>
