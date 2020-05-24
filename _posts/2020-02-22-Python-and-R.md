---
title: Python and R
date: 2020-02-22 12:28:12 -0500
img: python-r.jpg
comments: true
categories: [Programming]
tags: [python]
---

## Tools

### R Interface to Python

I found [reticulate](https://blog.rstudio.com/tags/reticulate) to be a pretty good tool. The following notes are for this tool. And the following implementations are in RStudio(R in terminal also works).

References:
- [reticulate](https://blog.rstudio.com/tags/reticulate)
- [RStudio IDE Tools for reticulate](https://rstudio.github.io/reticulate/articles/rstudio_ide.html)


#### Import a python module
Full path of python should be used in the `use_python` function. To find the path, use `which python` in the terminal.
``` r
library(reticulate)
use_python('/Users/yuyang/anaconda3/bin/python', required = TRUE)
pd <- import("pandas")
```



### Python Interface to R

- [rpy2](https://rpy2.bitbucket.io/)



