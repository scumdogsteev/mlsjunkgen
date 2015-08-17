<!-- README.md is generated from README.Rmd. Please edit that file -->
[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/mlsjunkgen)](http://cran.r-project.org/package=mlsjunkgen) [![Travis-CI Build Status](https://travis-ci.org/scumdogsteev/mlsjunkgen.svg?branch=master)](https://travis-ci.org/scumdogsteev/mlsjunkgen) [![Coverage Status](https://img.shields.io/coveralls/scumdogsteev/mlsjunkgen.svg)](https://coveralls.io/r/mlsjunkgen/mlsjunkgen?branch=master)

mlsjunkgen
==========

**`mlsjunkgen`** is an R package that generates pseudo-random numbers using the MLS Junk Generator algorithm (see below).

Author: Steve Myles (<steve@mylesandmyles.info>)

Project Home: <http://steve.mylesandmyles.info/projects/mls-junk-generator/>

License: MIT license

### Background

I took a course in graduate school ("[Statistical Analysis for Digital Simulation](http://www.depts.ttu.edu/officialpublications/courses/ie.php#ie_5000)") at [Texas Tech](http://www.ttu.edu/) from Dr. Elliot Montes where we spent a lot of time on the generation and analysis of random numbers. Here is a simple-yet-powerful pseudo-random number generator that I learned about in that course. It is named "The MLS Junk Generator" after [Dr. Milton L. Smith](http://www.depts.ttu.edu/ieweb/faculty/faculty.php?name=Milton%20Smith).

I have also released [an Excel/VBA implementation](https://github.com/scumdogsteev/mls-junk-generator) and provided [the simple R code](https://github.com/scumdogsteev/mls-junk-generatR) used as the basis for this package.

#### Algorithm

For any seed values of w, x, y, z:

r<sub>i</sub> = 5.980217w<sup>2</sup> + 9.446377x<sup>0.25</sup> + 4.81379y<sup>0.33</sup> + 8.91197z<sup>0.5</sup>

r<sub>i</sub> = r<sub>i</sub> - Int(r<sub>i</sub>)

For r<sub>i</sub>+1:

w = x

x = y

y = z

z = r<sub>i</sub>

#### Analysis

This generator tends to do well with various tests for randomness (K-S, Chi Square, test for runs up and down). It may not perform as well on other tests (e.g., tests for runs above and below the mean), but that could relate to my choice of seeds. As a point of reference, the period of Excel's built-in random number generator is 16,777,216 and the MLS Junk Generator's period is something greater than 9.9 billion (the point at which I gave up on trying to determine it).

### Installation

-   `mlsjunkgen` is available [on CRAN](http://cran.r-project.org/web/packages/mlsjunkgen/index.html) and can be installed accordingly:

    ``` r
    install.packages("mlsjunkgen")
    library(mlsjunkgen)
    ```

-   You can also install `mlsjunkgen` from GitHub using the `devtools` package:

    ``` r
    install.packages("devtools")
    library("devtools")
    install_github("scumdogsteev/mlsjunkgen")
    library(mlsjunkgen)
    ```

### Usage

The package consists of four functions:

1.  `junkgen` - generates a pseudo-random number from user-specified seeds
2.  `mlsjunkgenv` - generates a vector of pseudo-random numbers by calling `junkgen` a user-specified number of times
3.  `mlsjunkgend` - generates a data frame of pseudo-random numbers by calling `junkgen` a user-specified number of times
4.  `mlsjunkgenm` - generates a user-specified size matrix of pseudo-random numbers by calling `mlsjunkgenv` and assigning the results to a matrix

#### Examples

**`junkgen`** generates a single pseudo-random number based on four user-specified seeds:

``` r
w <- 1
x <- 2
y <- 3
z <- 4
junkgen(w = w, x = x, y = y, z = z)
#> [1] 0.9551644
```

**`mlsjunkgenv`** generates a vector containing a stream of `n` (default = 1) user-specified pseudo-random numbers based on four user-specified seeds rounded to a specified (default = 5) number of decimal places:

``` r
mlsjunkgenv(n = 10, w = w, x = x, y = y, z = z, round = 8)
#>  [1] 0.9551644 0.6690774 0.2123540 0.3448801 0.1199463 0.5639798 0.5923515
#>  [8] 0.1143156 0.3352500 0.7027079
```

The same example with default rounding:

``` r
mlsjunkgenv(n = 10, w = w, x = x, y = y, z = z)
#>  [1] 0.95516 0.66908 0.21235 0.34488 0.11995 0.56398 0.59235 0.11432
#>  [9] 0.33525 0.70271
```

**`mlsjunkgend`** generates a data frame containing a stream of `n` user-specified pseudo-random numbers based on four user-specified seeds:

``` r
mlsjunkgend(n = 10, w = w, x = x, y = y, z = z, round = 8)
#>           RN
#> 1  0.9551644
#> 2  0.6690774
#> 3  0.2123540
#> 4  0.3448801
#> 5  0.1199463
#> 6  0.5639798
#> 7  0.5923515
#> 8  0.1143156
#> 9  0.3352500
#> 10 0.7027079
```

The same example with default rounding:

``` r
mlsjunkgend(n = 10, w = w, x = x, y = y, z = z)
#>         RN
#> 1  0.95516
#> 2  0.66908
#> 3  0.21235
#> 4  0.34488
#> 5  0.11995
#> 6  0.56398
#> 7  0.59235
#> 8  0.11432
#> 9  0.33525
#> 10 0.70271
```

**`mlsjunkgenm`** generates a matrix of user-specified size containing a stream of pseudo-random numbers based on four user-specified seeds:

``` r
mlsjunkgenm(nrow = 5, ncol = 5, w = w, x = x, y = y, z = z, round = 3)
#>       [,1]  [,2]  [,3]  [,4]  [,5]
#> [1,] 0.955 0.564 0.418 0.052 0.020
#> [2,] 0.669 0.592 0.313 0.663 0.110
#> [3,] 0.212 0.114 0.920 0.802 0.685
#> [4,] 0.345 0.335 0.379 0.160 0.286
#> [5,] 0.120 0.703 0.280 0.586 0.452
```
