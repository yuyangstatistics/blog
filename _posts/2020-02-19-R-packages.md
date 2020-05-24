---
title: R Packages
date: 2020-02-19 12:28:12 -0500
categories: [Programming]
tags: [R]
---

### Create an R package
References:
- [Instructions for Creating Your Own R Package](http://web.mit.edu/insong/www/pdf/rpackage_instructions.pdf)
- [Warning about UTF-8 with roxygen2](https://stackoverflow.com/questions/51694929/warning-about-utf-8-with-roxygen2)
- [](https://stackoverflow.com/questions/29135971/namespace-not-generated-by-roxygen2-skipped-confusion-with-hadley-book)

Create from command line
1. Create a folder named 'greetings': `mkdir greetings` and `cd greetings`.
2. Write some R files in the folder, for example, `hello.R` and `goodbye.R`.(No C files.)
3. Open R script: `r --vanilla`, run `package.skeleton(name="greetings", code_files=c("hello.R", "goodbye.R"))`. Quit R, you will see a folder named `greetings`.
4. Change directory into `greetings`: `cd greetings`. Edit `DESCRIPTION` file, add `Encoding: UTF-8` to the end.
5. Remove `NAMESPACE` file: `rm NAMESPACE`. Open R script: `r --vanilla`, run `devtools::document()` to update the `NAMESPACE` file.
6. Edit `.Rd` files in the folder `man`, make sure `title` is edited. Remove the package rd file:`rm greetings-package.Rd`.
    If examples section is modified, then we need to add `export(func)` to `NAMESPACE`.
7. Check the functions are working and the pacakges are loaded correctly. Change directory to the original `greetings` folder, the one with a subdirectory `greetings` and the R files. Open R script: `r --vanilla`, run 
    ``` r
    library(devtools)
    library(roxygen2)
    my.Rpackage <- as.package("greetings")
    load_all(my.Rpackage)
    document(my.Rpackage)
    ```
8. Build, install, and check the package.
    ```
    R CMD build greetings
    R CMD INSTALL greetings_1.0.tar.gz
    R CMD check --as-cran greetings_1.0.tar.gz
    ```
9. Load the library in R script and try some functions.


### Edit .Rd files
1. Feel free to remove the .Rd files if you don't plan to export the corresponding functions.
2. Share one .Rd file. For example, use `xkcd.Rd` for `dxkcd.Rd, pxkcd.Rd, qxkcd.Rd, rxkcd.Rd`. 
    - Rename `dxkcd.Rd` with `xkcd.Rd`, and remove the other Rd files.
    - Use alias to relate the other functions to this .Rd file.
3. Check [Writing R documentation files](https://colinfay.me/writing-r-extensions/writing-r-documentation-files.html) detaild Rd file rendering.
4. View .Rd files conveniently. Go to the directory of the Rd file.
    ``` r
    library(Rdpack)
    viewRd('./xkcd.Rd', type='html')
    ```
    
### Do tests in the R package.
References:
- [Testing](http://r-pkgs.had.co.nz/tests.html) 

1. Get into the package directory, the one with `NAMESPACE`, with `cd greetings`. Open R script: `r --vanilla`.
    ```
    devtools::use_testthat()
    ```
    or 
    ```
    library(devtools)
    use_testthat()
    ```
    This will:
    - Create a `tests/testthat` directory in the package directory.
    - Adds testthat to the `Suggests` field in the `DESCRIPTION`.
    - Creates a file `tests/testthat.R` that runs all your tests when `R CMD check` runs. Do not need to modify `testthat.R`.
2. Move into the directory `tests/testthat`, and create test R files inside this directory. Each test R file serves for one single test. 
    - Every test file's name should start with `test`. 
    - Need to include `context()` to describe the usage of this test file.
    - When testing the equivalence of numbers, control the output precision when running it in R by `sprintf("%.20f", x)`, then paste the result to `expect_equal()`.
    - For other test statements, check the reference for more detail.
    - For example, create a test file `test_dxkcd.R` to test for `dxkcd` function.
        ```
        context("dxkcd")
        library(xkcd)

        test_that("the output is of the same length as max(len(y), len(sd.x))", {
        expect_equal(length(dxkcd(0.1, 1)), 1)
        expect_equal(length(dxkcd(0.1, c(1, 2, 3))), 3)
        expect_equal(length(dxkcd(c(0.1, 0.12), c(1, 1.5, 2, 2.5))), 4)
        expect_equal(length(dxkcd(c(0.1, 0.12, 0.13, 0.14), c(1, 1.5))), 4)
        })

        test_that("the output is correct within tolerance", {
            expect_equal(dxkcd(0.1, 1), 3.32703659106943439028)
        })
        ```
3. Run the tests. Change directory to the package directory, the one containing `NAMESPACE`. Open R script: `r --vanilla`.
    ```
    devtools::test()
    ```
    Correct mistakes refering to the prompt if there is any.


### Commit the package to Github
1. Remove the R files that are used to generate the package skeleton.
2. Add `.gitignore` file to the repository you want to commit. Check my [R.gitignore]( https://raw.githubusercontent.com/yuyang-yy/materials/master/config/R/R.gitignore).
3. Take the usual steps to commit.


### R's C Interface
References:
- [BST 140.776 Statistical Computing](http://www.biostat.jhsph.edu/~bcaffo/statcomp/)
    - [C Programming I](https://www.biostat.wisc.edu/~kbroman/teaching/statprog/cprog1_ho.pdf)
    - [C Programming II](https://www.biostat.wisc.edu/~kbroman/teaching/statprog/cprog2_ho.pdf)
    - [C Programming III](https://www.biostat.wisc.edu/~kbroman/teaching/statprog/cprog3_ho.pdf)


### Rcpp
References:
- [Instructions for Creating Your Own R Package](http://web.mit.edu/insong/www/pdf/rpackage_instructions.pdf)

Since there are so many subtle issue in Catalina, I turned to Ubuntu machine on Goolge Cloud. The installation of R follows the instruction [How to Install R on Ubuntu 18.04](https://linuxize.com/post/how-to-install-r-on-ubuntu-18-04/).

`sudo apt install libcurl4-openssl-dev`
`sudo apt install libxml2-dev`

Packages are installed as root `sudo -i R`, including:
- Rcpp, devtools, bench, conformalInference, 

### Build R packages with Rstudio

- Check [Instructions for Creating Your Own R Package](http://web.mit.edu/insong/www/pdf/rpackage_instructions.pdf) for detailed steps to build a package in Rstudio.
- Check [roxygen2 documentations](https://cran.r-project.org/web/packages/roxygen2/index.html) for instructions about roxygen2.
- Use `Ctrl + Shift + B` to quickly build, install, and reload.
- Add `*.Rproj` and `.Rbuildignore` to the `.gitignore` file when building a package using Rstudio.

#### About roxygen2 in Rstudio
- There is an icon above the R file, called `Code Tools`. Put the cursor inside the function you want to write a document, click the icon, and choose *Insert Roxygen Skeleton*.
- Add `Roxygen: list(markdown = TRUE)` to `DESCRIPTION` to enable markdown syntax in roxygen2.

#### About vignettes
1. Build vignettes following the instructions in [Writing vignettes](https://kbroman.org/pkg_primer/pages/vignettes.html).
2. The default comment setting is `"#>"`, and you can change it to `">"` if you prefer. And also the collapse setting.
3. html vignette saves memory, and this is why it is the default option. You can also choose to output to a pdf document by setting `output: pdf_document`.
4. `Ctrl + Shift + B` will not generate vignettes. To build the package with vignettes, use command line `R CMD build packagename` and `R CMD INSTALL tarballfile`. I tried using devtools to sovle this problem, I ran `devtools::build()` and `devtools::install(build_vignettes = TRUE)`. After doing this, we shall see the vignettes information by `browseVignettes("packagename")`. But everytime I do this, there would an error message when I try to see the help files. Command line is the best way for me so far.
5. `vignettes(package = "packagename")`: show the vignette information.
6. `browseVignettes("packagename")`: open the vignette files in a browser.

#### About datasets
1. First, create a folder `data/`, and then save the dataset in .rda format: `save(mydata, file="data/mydata.RData")`.
2. Second, create a file `mydata.R` in the `R/` folder, and write roxygen comments. Check [Rd (documentation) tags](https://cran.r-project.org/web/packages/roxygen2/vignettes/rd.html) and [Including datasets](https://kbroman.org/pkg_primer/pages/data.html) for detailed instructions.
3. Third, add `LazyData: true` to the `DESCRIPTION` file if it is not there.

#### Summary about steps after finishing editing files
``` r
library(devtools)
document()
test()
```

> R CMD build ...
>
> R CMD INSTALL ...
>
> R CMD check ...

``` r
library(package)
?function
browseVignettes("package")
```

