
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

``` r
# Croix:
library(classdata)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

1.  Inspect the first few lines of the data set

``` r
# Croix:
head(ames)
```

    ## # A tibble: 6 × 16
    ##   `Parcel ID` Address      Style Occupancy `Sale Date` `Sale Price` `Multi Sale`
    ##   <chr>       <chr>        <fct> <fct>     <date>             <dbl> <chr>       
    ## 1 0903202160  1024 RIDGEW… 1 1/… Single-F… 2022-08-12        181900 <NA>        
    ## 2 0907428215  4503 TWAIN … 1 St… Condomin… 2022-08-04        127100 <NA>        
    ## 3 0909428070  2030 MCCART… 1 St… Single-F… 2022-08-15             0 <NA>        
    ## 4 0923203160  3404 EMERAL… 1 St… Townhouse 2022-08-09        245000 <NA>        
    ## 5 0520440010  4507 EVERES… <NA>  <NA>      2022-08-03        449664 <NA>        
    ## 6 0907275030  4512 HEMING… 2 St… Single-F… 2022-08-16        368000 <NA>        
    ## # ℹ 9 more variables: YearBuilt <dbl>, Acres <dbl>,
    ## #   `TotalLivingArea (sf)` <dbl>, Bedrooms <dbl>,
    ## #   `FinishedBsmtArea (sf)` <dbl>, `LotArea(sf)` <dbl>, AC <chr>,
    ## #   FirePlace <chr>, Neighborhood <fct>

2.  Is there a variable of special interest? The variable of special
    interest is `Sale Price`.

3.  Start the exploration with the main variable:

What is the range of the variable? Draw a histogram for a numeric
variable or a bar chart, if the variable is categorical. What is the
general pattern? Is there anything odd? -Keegan: There is a skew right
and there are a couple outliers that cost way more than the rest of the
prices.

``` r
library(ggplot2)
library(classdata)

ggplot(data=ames, aes(x=`Sale Price`)) + geom_histogram(binwidth=100000) +
  labs(title="histogram", x = "sale price", y="count")
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
min(ames$'Sale Price')
```

    ## [1] 0

``` r
max(ames$'Sale Price')
```

    ## [1] 20500000

4.  Pick a variable that might be related to the main variable. what is
    the range of that variable? plot. describe the pattern.

Variable related: TotalLivingArea (sf)

``` r
# Croix: 
ggplot(data = ames, aes(x = `TotalLivingArea (sf)`)) + geom_histogram(binwidth = 500)
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
# Ji Xian Fu:
which.min(ames$`TotalLivingArea (sf)`)
```

    ## [1] 35

``` r
which.max(ames$`TotalLivingArea (sf)`)
```

    ## [1] 6482

``` r
ames$`TotalLivingArea (sf)`[35]
```

    ## [1] 0

``` r
ames$`TotalLivingArea (sf)`[6482]
```

    ## [1] 6007

Croix: The pattern of this histogram is unimodal and slightly skewed
right. Values to the far right may be potential outliers. The range of
this variable is from 0 square feet and 6007 square feet.

what is the relationship to the main variable? plot a scatterplot,
boxplot or facetted barcharts (dependening on the types of variables
involved). Describe overall pattern, does this variable describe any
oddities discovered in 3? Identify/follow-up on any oddities.

``` r
#Allison
ggplot(data = ames, aes(x = `TotalLivingArea (sf)`, y = `Sale Price`)) + geom_point()
```

    ## Warning: Removed 447 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-7-1.png)<!-- --> Allison: It
looks like there is no direct relationship between TotalLivingArea (sf)
and Sale Price. All sale prices stay towards the bottom of the graph and
do not show a positive or negative linear relation. This variable does
not describe any of the oddities shown in step 3, as the extremely high
sale prices are actually for fairly low square footage areas.

Ji Xian Fu - Procedure: The main variable for this exploration is Sale
Price. As a team, do steps 1 through 3. Document your findings in the
README.Rmd of the lab’s repo.

As a team, discuss different lines of investigation (step 4) and agree
on who is doing which investigation. Make a note of who is doing what in
the README.Rmd

Individually: follow through with your line of investigation. Include at
least one plot that describes the relationship between sales prices and
your variable. Include one paragraph describing the pattern you see. Are
there oddities? Follow-up on (some of) them.
