---
title: Technical Problems collection
date: 2018-08-08 12:28:12 -0500
img: terminal.jpg
categories: [System]
tags: [terminal]
---

## Probelms about the environment variables.

1. I installed the new version of R and Rstudio on the mac, but every time I open the Rstudio, 
the following warning messages would appear:
```
1: Setting LC_CTYPE failed, using "C"
2: Setting LC_COLLATE failed, using "C"
3: Setting LC_TIME failed, using "C"
4: Setting LC_MESSAGES failed, using "C"
5: Setting LC_PAPER failed, using "C"
```
After reading the guidance on the [stackoverflow post](https://stackoverflow.com/questions/9689104/installing-r-on-mac-warning-messages-setting-lc-ctype-failed-using-c), I write the following code on the terminal and problem got solved.
```
defaults write org.R-project.R force.LANG en_US.UTF-8
```

2. To use the LightGBM for multi-threading, I installed OpenMP. But after that, I cannot use XGBoost again. Not after restarting the computer and reinstall the package on Anaconda. Whenever I tried to import XGBoost, the following error would occur:
```
/anaconda3/lib/python3.6/site-packages/xgboost/core.py in <module>()
    134 
    135 # load the XGBoost library globally
```
The posts said it's due to the gcc version. To solve this problem, I referenced [github post](https://github.com/dmlc/xgboost/issues/1442) and [Installing XGBoost on Mac OSX](https://www.ibm.com/developerworks/community/blogs/jfp/entry/Installing_XGBoost_on_Mac_OSX?lang=en) to fix this problem.

The gcc version of my mac is 8, so I used the following code.
```
export CC = gcc-8
export CXX = g++-8
```
I tried to use `gcc --version`, but the result is version 9, which is not right. So I tried to use `brew install gcc` and it told me the version is 8.

By the way, the directory of anaconda packages is 
```
/anaconda3/lib/python3.6/site-packages/
```

And when I got everything done, I could import xgboost, but cannot import plot_importance from xgboost. The way I solved this is to restart the jupyter notebook and it worked.

Similar thing happens to lightgbm. So I used `conda uninstall lightgbm` to uninstall it and then install it from the binary source. Reference is the [Microsoft/LightGBM](https://github.com/Microsoft/LightGBM/issues/1369). And since I don't have *cmake*, I used `brew install cmake` to install it.
```
conda uninstall lightgbm
git clone --recursive https://github.com/Microsoft/LightGBM ; cd LightGBM
export CXX=g++-8 CC=gcc-8
mkdir build ; cd build
cmake ..
make -j4
```
However, error eccurs at this time, so the final decision is to uninstall it and use conda to reinstall lightgbm. The thing is the openmp will be downgraded. This is an open question.
