Data Reshaping Cheatsheet
================

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(nycflights13))
```

===

This is a cheat sheet for **Data Reshaping** mainly for myself, but hopefully could be the reference sheet for new R programmers. For simple reshaping, the following functions from **tidyr** are the following:

| tidyr Function | Definition                                                 |
|----------------|------------------------------------------------------------|
| `gather`       | takes multiple columns and collapses into key values pairs |
| `spread`       | Spread a key-value pair across multiple columns            |

Demo for these two main functions in `tidyr`
--------------------------------------------

This demo is first presented using simple example and then presented using database **nycflights13**, which is the flights departing NYC in 2013. Several example of usage are shown below:

There are several tibbles in package **nycflights13**: `flights`,`weather`,`planes`,`airports`,`airlines`. For further information of this dataset can refer to: [`nycflights13`](https://cran.r-project.org/web/packages/nycflights13/nycflights13.pdf)
