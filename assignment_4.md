Assignment 4
================

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(gridExtra))
```

Exploring gather() and spread() for data reshaping
--------------------------------------------------

The prompt I have chosen to explore is acivity 2:

-   Make a tibble with one row per year and columns for life expectancy for two or more countries.
-   Use `knitr::kable()` to make this table look pretty in your rendered homework. Take advantage of this new data shape to scatterplot life expectancy for one country against that of another.

First, we explore the dataset `gapminder` and check the range of the year. Then we choose three country Canada ,Mexico and China and store their life-expectancy data in the new variable new\_exp.

``` r
head(gapminder)
```

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

``` r
range(gapminder$year)
```

    ## [1] 1952 2007

``` r
## we first extract the life expectancy data for these three country from the gapminder dataset 
temp <- gapminder %>% 
  select(country,lifeExp,year) %>% 
  filter(country == "Canada" | country == "China" | country == "Mexico") 
 
# then a tibble is created with year, country and lifeExp
tidy_ver <- tibble(year=temp$year,country=temp$country,lifeExp=temp$lifeExp)
knitr::kable(tidy_ver)
```

|  year| country |   lifeExp|
|-----:|:--------|---------:|
|  1952| Canada  |  68.75000|
|  1957| Canada  |  69.96000|
|  1962| Canada  |  71.30000|
|  1967| Canada  |  72.13000|
|  1972| Canada  |  72.88000|
|  1977| Canada  |  74.21000|
|  1982| Canada  |  75.76000|
|  1987| Canada  |  76.86000|
|  1992| Canada  |  77.95000|
|  1997| Canada  |  78.61000|
|  2002| Canada  |  79.77000|
|  2007| Canada  |  80.65300|
|  1952| China   |  44.00000|
|  1957| China   |  50.54896|
|  1962| China   |  44.50136|
|  1967| China   |  58.38112|
|  1972| China   |  63.11888|
|  1977| China   |  63.96736|
|  1982| China   |  65.52500|
|  1987| China   |  67.27400|
|  1992| China   |  68.69000|
|  1997| China   |  70.42600|
|  2002| China   |  72.02800|
|  2007| China   |  72.96100|
|  1952| Mexico  |  50.78900|
|  1957| Mexico  |  55.19000|
|  1962| Mexico  |  58.29900|
|  1967| Mexico  |  60.11000|
|  1972| Mexico  |  62.36100|
|  1977| Mexico  |  65.03200|
|  1982| Mexico  |  67.40500|
|  1987| Mexico  |  69.49800|
|  1992| Mexico  |  71.45500|
|  1997| Mexico  |  73.67000|
|  2002| Mexico  |  74.90200|
|  2007| Mexico  |  76.19500|

``` r
# then we would like to form an untidy tibble by separating the data by country
 result <- spread(tidy_ver, key = "country", value = "lifeExp")
 knitr::kable(result)
```

|  year|  Canada|     China|  Mexico|
|-----:|-------:|---------:|-------:|
|  1952|  68.750|  44.00000|  50.789|
|  1957|  69.960|  50.54896|  55.190|
|  1962|  71.300|  44.50136|  58.299|
|  1967|  72.130|  58.38112|  60.110|
|  1972|  72.880|  63.11888|  62.361|
|  1977|  74.210|  63.96736|  65.032|
|  1982|  75.760|  65.52500|  67.405|
|  1987|  76.860|  67.27400|  69.498|
|  1992|  77.950|  68.69000|  71.455|
|  1997|  78.610|  70.42600|  73.670|
|  2002|  79.770|  72.02800|  74.902|
|  2007|  80.653|  72.96100|  76.195|

The data appeared under each country represented the life-expectancy of the corresponding country. To tidy up the above data, we could simply use the gather() function to reverse the process as shown below:

``` r
reverse <-  gather(result,key="country",value="life_Expectancy", China, Mexico,Canada)
head(reverse)
```

    ## # A tibble: 6 x 3
    ##    year country life_Expectancy
    ##   <int> <chr>             <dbl>
    ## 1  1952 China              44  
    ## 2  1957 China              50.5
    ## 3  1962 China              44.5
    ## 4  1967 China              58.4
    ## 5  1972 China              63.1
    ## 6  1977 China              64.0

The following step is to visualise the data with the scatterplot using these reshaped data. Here shows the pairwise comparison of life expectancy among these three country.Meanwhile, the different color stands for data from the different year.

``` r
p1 <- result %>% 
  ggplot(aes(Canada, China))+
  geom_point(aes(colour=year))

p2 <- result %>% 
  ggplot(aes(Mexico, China))+
  geom_point(aes(color=year))

p3 <- result %>% 
  ggplot(aes(Canada, Mexico))+
  geom_point(aes(color=year))
grid.arrange(p1,p2,p3,nrow=2,ncol=2)
```

![](assignment_4_files/figure-markdown_github/unnamed-chunk-4-1.png)
