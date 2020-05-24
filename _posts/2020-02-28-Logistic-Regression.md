---
title: Logistic Regression
date: 2020-02-28 12:28:12 -0500
categories: [Statistics]
tags: [logistic]
---

## Parameter Estimate
The parameters are estimated by maximum likelihood estimate. 
- When we assume $p$ is a constant, $L = \prod_{i=1}^{n} p^{y_{i}}(1-p)^{1-y_{i}}$, then $\hat{p}=n^{-1} \sum_{i=1}^{n} y_{i}$.
- When we assume each trial has its own sucess probability $p_i$, $L = \prod_{i=1}^{n} p_{i}^{y_{i}}\left(1-p_{i}\right)^{1-y_i}$, then the model is not estimable.
- As a remedy, we consider using $\theta$ as the parameter for $p_i$, namely, $p_i = p(x_i, \theta)$. When $x_i$ are the same, $p_i$ would be the same. Now, the model would be estimable with $\theta$ having lower dimension than the sample size $n$.

References:
- [Logistic Regression Lecutre Notes](https://www.stat.cmu.edu/~cshalizi/uADA/12/lectures/ch12.pdf)


---------------------------------------

## Smoothing of Binary variables

References:
- Cook, R. Dennis, and Sanford Weisberg. “Graphics for Assessing the Adequacy of Regression Models.” Journal of the American Statistical Association, vol. 92, no. 438, 1997, pp. 490–499. JSTOR, www.jstor.org/stable/2965698. Accessed 28 Feb. 2020.

After reading Cooks and Weisberg's paper, I would like to try it on a classification problem.  They proposed to use lowess to smooth data, so I would just follow what they did.

For numerical response, there would be no issues and we just need to use `stats::lowess()` in R. But for categorical response, things might be more tricky.