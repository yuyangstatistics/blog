---
title: Rmarkdown Notes
date: 2018-08-30 12:28:12 -0500
img: rmarkdown.jpg
categories: [Tools]
tags: [rmarkdown]
---

The following notes are referenced from the [R Documentation](https://rmarkdown.rstudio.com/lesson-1.html)

1. To run an rmarkdown file, you can either use 
```{r}
library(rmarkdown)
render("rmarkdown-notes.rmd")  # this should be path of the rmd file
```
Or, you can just use the **Knit** button on the bar of RStudio or use keyboard shortcut `⇧⌘K`.

2. How RMarkdown works. 

> rmd -> knitr -> md -> pandoc -> final format

3. Generate a table, for example, the ANOVA table.
    - Directly input the following code.
    ```{rmarkdown}
    |Source |DF      |   SS|   MS|F     |
    |:------|:-------|----:|----:|:-----|
    |Trt    |g-1 = 5 | 9.65| 1.93|15.45 |
    |Error  |N-g=18  | 2.25| 0.12|      |
    ```
    - Use knitr library in the r code block.
    ```{r}
    library(knitr)
    anovatable <- data.frame(Source = c("Trt", "Error"), DF = c("g-1 = 5", "N-g=18"),                           SS = c(9.65, 2.25), MS = c(1.93, 0.12), F = c(15.45,""))
    kable(anovatable, caption = "ANOVA")
    ```
