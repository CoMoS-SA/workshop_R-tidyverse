Tidy modelling
================
Matteo Sostero

Packages for this session
-------------------------

| package       | purpose                    | installation |
|---------------|----------------------------|--------------|
| *tidyverse*   | everything                 | CRAN         |
| *nycflight13* | example datasets           | CRAN         |
| *broom*       | tidying statistical models | CRAN         |

If not yet installed, download packages with `install.packages("name")`. If asked, **do not compile from source**.

Load the packages for the session:

``` r
# *tidyverse* loads the core packages of the *tidyverse* and shows their version.
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.4
    ## v tibble  1.4.2     v dplyr   0.7.4
    ## v tidyr   0.8.0     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts ------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(nycflights13)
library(broom)
```

Model evaluation and tidying
----------------------------

``` r
data(flights)

flights %>%
  split(.$month) %>%
  set_names(month.name) %>%
  map(~ lm(dep_delay ~ dep_time + day, data = .)) %>%
  map_dfr(~ tidy(.), .id = "chunk")
```

    ##        chunk        term     estimate    std.error   statistic
    ## 1    January (Intercept) -17.57879821 0.7557414366 -23.2603340
    ## 2    January    dep_time   0.01635145 0.0004538042  36.0319479
    ## 3    January         day   0.35250996 0.0243393075  14.4831548
    ## 4   February (Intercept) -13.78718700 0.7972979897 -17.2923890
    ## 5   February    dep_time   0.01669014 0.0004756105  35.0920283
    ## 6   February         day   0.14126986 0.0282694771   4.9972575
    ## 7      March (Intercept)  -6.57028664 0.8059688802  -8.1520351
    ## 8      March    dep_time   0.01851036 0.0004747735  38.9877795
    ## 9      March         day  -0.33259055 0.0261941741 -12.6971190
    ## 10     April (Intercept) -19.83222090 0.8506549365 -23.3140608
    ## 11     April    dep_time   0.02267219 0.0005055018  44.8508553
    ## 12     April         day   0.20038595 0.0285666322   7.0146858
    ## 13       May (Intercept) -20.77830790 0.7666571275 -27.1024780
    ## 14       May    dep_time   0.02357960 0.0004570829  51.5871332
    ## 15       May         day   0.11951175 0.0248573852   4.8078973
    ## 16      June (Intercept) -36.06046344 0.9907440433 -36.3973558
    ## 17      June    dep_time   0.03290560 0.0005787463  56.8566966
    ## 18      June         day   0.80496447 0.0342784242  23.4831236
    ## 19      July (Intercept) -15.04211591 0.9779901838 -15.3806410
    ## 20      July    dep_time   0.03191745 0.0005704413  55.9522109
    ## 21      July         day  -0.39573148 0.0324972115 -12.1773979
    ## 22    August (Intercept) -11.40202258 0.7294940172 -15.6300426
    ## 23    August    dep_time   0.02127409 0.0004304610  49.4216444
    ## 24    August         day  -0.29677459 0.0239688557 -12.3816752
    ## 25 September (Intercept) -10.56925366 0.7344320911 -14.3910564
    ## 26 September    dep_time   0.01684061 0.0004426229  38.0472993
    ## 27 September         day  -0.33039906 0.0244044955 -13.5384506
    ## 28   October (Intercept) -12.12059288 0.5885113108 -20.5953440
    ## 29   October    dep_time   0.01644192 0.0003550737  46.3056501
    ## 30   October         day  -0.22926318 0.0187823288 -12.2063235
    ## 31  November (Intercept) -13.58602110 0.5724779348 -23.7319559
    ## 32  November    dep_time   0.01284492 0.0003444952  37.2862063
    ## 33  November         day   0.11451230 0.0192706339   5.9423213
    ## 34  December (Intercept) -12.76039163 0.8440695988 -15.1177008
    ## 35  December    dep_time   0.02192509 0.0005022639  43.6525389
    ## 36  December         day  -0.02644830 0.0272913285  -0.9691102
    ##          p.value
    ## 1  1.725964e-118
    ## 2  1.336969e-277
    ## 3   2.349698e-47
    ## 4   1.377144e-66
    ## 5  4.791050e-263
    ## 6   5.856552e-07
    ## 7   3.726743e-16
    ## 8  9.881313e-324
    ## 9   7.754270e-37
    ## 10 4.499062e-119
    ## 11  0.000000e+00
    ## 12  2.357670e-12
    ## 13 1.022083e-159
    ## 14  0.000000e+00
    ## 15  1.533109e-06
    ## 16 2.882191e-283
    ## 17  0.000000e+00
    ## 18 9.632636e-121
    ## 19  3.612865e-53
    ## 20  0.000000e+00
    ## 21  4.984389e-34
    ## 22  7.634812e-55
    ## 23  0.000000e+00
    ## 24  4.034090e-35
    ## 25  8.760656e-47
    ## 26 1.240257e-308
    ## 27  1.266339e-41
    ## 28  1.440660e-93
    ## 29  0.000000e+00
    ## 30  3.497352e-34
    ## 31 3.078575e-123
    ## 32 9.045685e-297
    ## 33  2.844538e-09
    ## 34  2.007000e-51
    ## 35  0.000000e+00
    ## 36  3.324989e-01
