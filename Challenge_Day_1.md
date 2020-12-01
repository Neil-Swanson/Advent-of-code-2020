Day 1 - Report Repair
================

# Background

Source of the daily challenge comes from the [Advent of Code
for 2020](https://adventofcode.com/) produced by [Eric
Wastl](https://twitter.com/ericwastl).

## Challenge

Find two numbers in the expense report that sum to 2020 and multiply the
two numbers together.

## Data Source

The source of data in the expense report comes from:
<https://adventofcode.com/2020/day/1/input>

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

## Data management

Read in data from the [advent of code
website](https://adventofcode.com/2020/day/1/input):

``` r
d <- read.csv('Data/input_Day1.txt', header = F, col.names = 'expense', colClasses = 'numeric')
head(d)
```

    ##   expense
    ## 1    1509
    ## 2    1857
    ## 3    1736
    ## 4    1815
    ## 5    1576
    ## 6    1970

## Analysis

### Find two numbers that add to 2020

Print summary statistics for the dataset

``` r
summary(d)
```

    ##     expense    
    ##  Min.   :  48  
    ##  1st Qu.:1508  
    ##  Median :1722  
    ##  Mean   :1618  
    ##  3rd Qu.:1836  
    ##  Max.   :2010

Based on the minimum value of 48, we can remove all expenses greater
than 1972 since the sum would exceed 2020.

``` r
cd <- d %>%
  filter(expense <= 1972)
```

Loop through possible expense summations to see which two expenses add
to 2020.

``` r
exp_list <- sort(cd$expense)

i <- c()

for(i in exp_list){
  j <- 2020-i
  if(j %in% exp_list){
    print(c(i,j))
    break()
  }
}
```

    ## [1]  251 1769

Expenses of 251 and 1769 add to 2020.

### Multiply these two numbers together

``` r
exp_mult <- i*j
```

The final result is:

``` r
print(exp_mult)
```

    ## [1] 444019
