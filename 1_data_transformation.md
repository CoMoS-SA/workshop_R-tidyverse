Data transformation with dplyr
================
Matteo Sostero

Load the tidyverse package
--------------------------

``` r
library(tidyverse)
```

Load example data
-----------------

The *nycflights13* package contains different example datasets, including *flights*

``` r
library(nycflights13)
data(flights)
```

Preview, `glimpse` and `View` data
----------------------------------

Preview the data by invoking it: notice that not all variables are displayed for lack of space.

``` r
flights
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

`glimpse` shows all variables as rows, variable types, and a preview of first few observations.

``` r
glimpse(flights)
```

    ## Observations: 336,776
    ## Variables: 19
    ## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,...
    ## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 55...
    ## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 60...
    ## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2...
    ## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 7...
    ## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 7...
    ## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -...
    ## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV",...
    ## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79...
    ## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN...
    ## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR"...
    ## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL"...
    ## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138...
    ## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 94...
    ## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5,...
    ## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, ...
    ## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013...

`View` shows the whole dataset in a dedicated tab of RStudio

``` r
View(flights)
```

`filter` rows matching conditions
---------------------------------

Keep only observations such that month = 1 AND day = 1

``` r
flights %>% filter(month == 1, day == 1)
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 832 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

Logical operators include:

-   `==` strict equality
-   `>`, `<`, `>=`, `<=` inequalities
-   `%in%` to test if element belongs to list
-   `is.na()` to test for missing value `NA`

Multiple conditions:

-   `!` as logical NOT
-   `,` or `&` as logical AND

``` r
flights %>% filter(month %in% c(1,2))
```

    ## # A tibble: 51,955 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 51,945 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

`select` and `pull` variables
=============================

We can select columns by name; the result is always a tibble. Pressing TAB with the cursorinside `select( )` provides variable name completion.

``` r
flights %>% select(year, month, day, dep_time)
```

    ## # A tibble: 336,776 x 4
    ##     year month   day dep_time
    ##    <int> <int> <int>    <int>
    ##  1  2013     1     1      517
    ##  2  2013     1     1      533
    ##  3  2013     1     1      542
    ##  4  2013     1     1      544
    ##  5  2013     1     1      554
    ##  6  2013     1     1      554
    ##  7  2013     1     1      555
    ##  8  2013     1     1      557
    ##  9  2013     1     1      557
    ## 10  2013     1     1      558
    ## # ... with 336,766 more rows

We can also select columns based on patterns in their names:

``` r
flights %>% select(contains("dep"), starts_with("sched"))
```

    ## # A tibble: 336,776 x 4
    ##    dep_time sched_dep_time dep_delay sched_arr_time
    ##       <int>          <int>     <dbl>          <int>
    ##  1      517            515         2            819
    ##  2      533            529         4            830
    ##  3      542            540         2            850
    ##  4      544            545        -1           1022
    ##  5      554            600        -6            837
    ##  6      554            558        -4            728
    ##  7      555            600        -5            854
    ##  8      557            600        -3            723
    ##  9      557            600        -3            846
    ## 10      558            600        -2            745
    ## # ... with 336,766 more rows

or select intervals based on position (careful!)

``` r
flights %>% select(year:day)
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # ... with 336,766 more rows

`pull()` returns a single column as a vector or values

``` r
flights %>% pull(carrier)
```

    ##   [1] "UA" "UA" "AA" "B6" "DL" "UA" "B6" "EV" "B6" "AA" "B6" "B6" "UA" "UA"
    ##  [15] "AA" "B6" "UA" "B6" "MQ" "B6" "DL" "MQ" "AA" "DL" "UA" "MQ" "UA" "B6"
    ##  [29] "B6" "DL" "US" "AA" "UA" "EV" "MQ" "US" "AA" "UA" "AA" "WN" "US" "EV"
    ##  [43] "AA" "B6" "B6" "UA" "US" "UA" "B6" "UA" "UA" "B6" "B6" "DL" "DL" "DL"
    ##  [57] "DL" "AA" "AA" "MQ" "UA" "DL" "DL" "VX" "AA" "B6" "DL" "UA" "UA" "B6"
    ##  [71] "UA" "B6" "AA" "UA" "FL" "B6" "UA" "AA" "AS" "AA" "UA" "UA" "VX" "B6"
    ##  [85] "B6" "UA" "B6" "B6" "AA" "UA" "B6" "AA" "B6" "DL" "AA" "UA" "MQ" "DL"
    ##  [99] "UA" "US" "AA" "DL" "WN" "B6" "DL" "DL" "MQ" "B6" "AA" "UA" "DL" "B6"
    ## [113] "B6" "MQ" "DL" "EV" "9E" "DL" "EV" "MQ" "US" "EV" "DL" "FL" "B6" "B6"
    ## [127] "DL" "DL" "B6" "MQ" "EV" "US" "UA" "AA" "B6" "AA" "UA" "B6" "UA" "UA"
    ## [141] "UA" "AA" "MQ" "EV" "MQ" "F9" "AA" "MQ" "AA" "DL" "B6" "MQ" "UA" "EV"
    ## [155] "DL" "UA" "WN" "B6" "DL" "AA" "DL" "UA" "HA" "DL" "DL" "UA" "MQ" "DL"
    ## [169] "VX" "UA" "UA" "MQ" "UA" "B6" "UA" "B6" "US" "UA" "AA" "AA" "UA" "UA"
    ## [183] "AA" "UA" "AA" "B6" "B6" "B6" "MQ" "DL" "B6" "B6" "B6" "UA" "DL" "EV"
    ## [197] "WN" "UA" "B6" "UA" "VX" "B6" "B6" "WN" "DL" "DL" "B6" "WN" "AA" "MQ"
    ## [211] "B6" "EV" "B6" "EV" "MQ" "UA" "US" "DL" "UA" "DL" "US" "B6" "US" "UA"
    ## [225] "MQ" "DL" "US" "US" "EV" "DL" "FL" "EV" "MQ" "AA" "UA" "AA" "UA" "AA"
    ## [239] "EV" "VX" "UA" "EV" "UA" "AA" "UA" "B6" "EV" "UA" "UA" "AA" "DL" "MQ"
    ## [253] "B6" "DL" "EV" "DL" "US" "WN" "MQ" "UA" "B6" "DL" "UA" "MQ" "AA" "B6"
    ## [267] "UA" "DL" "UA" "EV" "WN" "UA" "B6" "DL" "US" "EV" "UA" "UA" "UA" "AA"
    ## [281] "DL" "MQ" "B6" "VX" "AA" "DL" "UA" "EV" "FL" "EV" "EV" "B6" "DL" "B6"
    ## [295] "MQ" "AA" "DL" "DL" "MQ" "EV" "MQ" "UA" "AA" "WN" "UA" "US" "EV" "UA"
    ## [309] "EV" "VX" "B6" "UA" "EV" "B6" "EV" "MQ" "UA" "AA" "DL" "WN" "EV" "B6"
    ## [323] "UA" "EV" "DL" "UA" "AA" "WN" "EV" "AA" "MQ" "EV" "DL" "DL" "B6" "UA"
    ## [337] "B6" "AA" "UA" "DL" "WN" "MQ" "US" "US" "B6" "MQ" "FL" "AA" "AA" "MQ"
    ## [351] "UA" "B6" "UA" "EV" "B6" "MQ" "AA" "WN" "B6" "US" "EV" "EV" "MQ" "EV"
    ## [365] "B6" "UA" "DL" "DL" "VX" "UA" "EV" "B6" "EV" "B6" "AA" "B6" "AA" "EV"
    ## [379] "AA" "UA" "WN" "EV" "B6" "EV" "EV" "EV" "DL" "EV" "B6" "WN" "MQ" "UA"
    ## [393] "UA" "UA" "US" "EV" "DL" "EV" "FL" "B6" "UA" "UA" "MQ" "B6" "B6" "DL"
    ## [407] "MQ" "UA" "EV" "EV" "EV" "B6" "UA" "UA" "B6" "UA" "DL" "DL" "DL" "DL"
    ## [421] "AA" "EV" "AA" "MQ" "AA" "US" "MQ" "9E" "9E" "B6" "MQ" "US" "EV" "9E"
    ## [435] "DL" "B6" "B6" "DL" "UA" "UA" "UA" "US" "MQ" "EV" "UA" "B6" "UA" "EV"
    ## [449] "MQ" "AA" "UA" "9E" "MQ" "UA" "B6" "DL" "DL" "B6" "EV" "MQ" "B6" "UA"
    ## [463] "AA" "MQ" "UA" "DL" "MQ" "UA" "UA" "B6" "B6" "MQ" "WN" "AA" "B6" "B6"
    ## [477] "UA" "EV" "AA" "UA" "US" "9E" "EV" "EV" "UA" "EV" "WN" "DL" "AA" "AA"
    ## [491] "UA" "B6" "DL" "DL" "UA" "9E" "DL" "MQ" "EV" "UA" "9E" "EV" "FL" "9E"
    ## [505] "AA" "9E" "DL" "MQ" "EV" "DL" "UA" "EV" "EV" "B6" "DL" "9E" "UA" "DL"
    ## [519] "EV" "B6" "WN" "MQ" "UA" "MQ" "AA" "B6" "UA" "AA" "AA" "B6" "DL" "DL"
    ## [533] "DL" "UA" "EV" "MQ" "UA" "DL" "US" "AA" "B6" "DL" "B6" "VX" "EV" "DL"
    ## [547] "EV" "B6" "EV" "US" "UA" "WN" "MQ" "UA" "UA" "B6" "9E" "EV" "MQ" "AA"
    ## [561] "UA" "EV" "EV" "B6" "B6" "AA" "DL" "EV" "DL" "EV" "AA" "DL" "VX" "AA"
    ## [575] "WN" "UA" "MQ" "AA" "UA" "UA" "AA" "US" "DL" "UA" "WN" "EV" "B6" "B6"
    ## [589] "UA" "UA" "B6" "AA" "F9" "B6" "UA" "AA" "B6" "MQ" "DL" "US" "UA" "AA"
    ## [603] "UA" "AA" "EV" "UA" "FL" "B6" "UA" "EV" "B6" "B6" "DL" "DL" "DL" "MQ"
    ## [617] "DL" "9E" "B6" "B6" "DL" "WN" "B6" "UA" "B6" "WN" "B6" "UA" "EV" "DL"
    ## [631] "B6" "B6" "UA" "EV" "B6" "UA" "DL" "UA" "EV" "MQ" "US" "UA" "MQ" "UA"
    ## [645] "AS" "B6" "UA" "EV" "B6" "EV" "WN" "MQ" "UA" "AA" "AA" "DL" "AA" "9E"
    ## [659] "US" "AA" "DL" "UA" "EV" "UA" "EV" "9E" "UA" "MQ" "UA" "EV" "B6" "MQ"
    ## [673] "UA" "EV" "UA" "AA" "DL" "DL" "AA" "AA" "AA" "FL" "EV" "9E" "VX" "US"
    ## [687] "MQ" "DL" "UA" "AA" "B6" "DL" "WN" "EV" "DL" "B6" "DL" "UA" "DL" "DL"
    ## [701] "B6" "DL" "EV" "9E" "US" "MQ" "DL" "UA" "DL" "UA" "AA" "EV" "DL" "EV"
    ## [715] "B6" "EV" "DL" "AA" "9E" "UA" "DL" "MQ" "EV" "AA" "EV" "9E" "AA" "UA"
    ## [729] "B6" "MQ" "9E" "EV" "B6" "EV" "VX" "UA" "9E" "9E" "B6" "UA" "DL" "UA"
    ## [743] "EV" "9E" "AA" "UA" "EV" "UA" "MQ" "MQ" "EV" "UA" "AA" "9E" "EV" "MQ"
    ## [757] "9E" "B6" "UA" "FL" "B6" "9E" "B6" "DL" "UA" "EV" "B6" "WN" "EV" "AA"
    ## [771] "B6" "B6" "UA" "UA" "UA" "EV" "B6" "9E" "UA" "MQ" "B6" "B6" "MQ" "UA"
    ## [785] "EV" "EV" "B6" "MQ" "MQ" "EV" "WN" "UA" "MQ" "B6" "UA" "DL" "B6" "UA"
    ## [799] "B6" "MQ" "EV" "9E" "EV" "EV" "B6" "B6" "MQ" "AA" "MQ" "B6" "UA" "B6"
    ## [813] "B6" "B6" "EV" "AA" "B6" "B6" "B6" "B6" "B6" "EV" "EV" "B6" "B6" "B6"
    ## [827] "EV" "B6" "B6" "B6" "EV" "EV" "B6" "B6" "EV" "B6" "B6" "B6" "EV" "AA"
    ## [841] "AA" "B6" "B6" "B6" "US" "UA" "AA" "UA" "B6" "B6" "B6" "B6" "AA" "B6"
    ## [855] "DL" "EV" "DL" "DL" "FL" "UA" "UA" "UA" "EV" "EV" "9E" "B6" "WN" "MQ"
    ## [869] "UA" "US" "AA" "UA" "UA" "DL" "DL" "AA" "B6" "EV" "DL" "WN" "B6" "B6"
    ## [883] "UA" "US" "AA" "MQ" "MQ" "MQ" "UA" "UA" "US" "DL" "WN" "EV" "EV" "US"
    ## [897] "B6" "DL" "WN" "EV" "UA" "AA" "UA" "UA" "EV" "US" "UA" "B6" "UA" "EV"
    ## [911] "AA" "B6" "B6" "US" "UA" "UA" "US" "DL" "UA" "DL" "UA" "AA" "B6" "DL"
    ## [925] "DL" "DL" "B6" "MQ" "US" "VX" "EV" "AA" "AA" "DL" "UA" "B6" "DL" "UA"
    ## [939] "AA" "MQ" "AA" "B6" "DL" "UA" "AA" "B6" "UA" "UA" "MQ" "AS" "UA" "VX"
    ## [953] "UA" "UA" "FL" "B6" "DL" "B6" "AA" "B6" "UA" "B6" "B6" "WN" "UA" "B6"
    ## [967] "AA" "AA" "UA" "WN" "EV" "UA" "9E" "DL" "AA" "UA" "B6" "UA" "9E" "EV"
    ## [981] "EV" "UA" "EV" "DL" "B6" "B6" "DL" "DL" "US" "AA" "B6" "DL" "AA" "MQ"
    ## [995] "UA" "AA" "DL" "DL" "US"
    ##  [ reached getOption("max.print") -- omitted 335777 entries ]

We can combine this with `sort` (lexicographic sorting) and `unique` (deduplication) to see unique observations:

``` r
flights %>% pull(carrier) %>% sort() %>% unique()
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

`summarise` values
------------------

We can compute one or more variable summaries for the whole dataset (column-wise) using `summarise`.

`mean(., na.rm = TRUE)` computes the average value, excluding missing values.

``` r
flights %>% 
  summarise(
    avg_dep_delay = mean(dep_delay, na.rm = TRUE),
    avg_arr_delay = mean(arr_delay, na.rm = TRUE)
  )
```

    ## # A tibble: 1 x 2
    ##   avg_dep_delay avg_arr_delay
    ##           <dbl>         <dbl>
    ## 1          12.6          6.90

How many missing values are there?

``` r
flights %>% 
  summarise(
    n_miss_dep_delay = sum(is.na(dep_delay)),
    n_miss_arr_delay = sum(is.na(arr_delay))
    )
```

    ## # A tibble: 1 x 2
    ##   n_miss_dep_delay n_miss_arr_delay
    ##              <int>            <int>
    ## 1             8255             9430

This works because `is.na(dep_delay)` returns a *logical vector* (TRUE, FALSE) for all values of `dep_delay`. `sum` adds the TRUE values:

``` r
flights %>% pull(dep_delay) %>% is.na() %>% sum()
```

    ## [1] 8255

`group_by` summarises the values by groups:

``` r
flights %>% 
  group_by(carrier) %>% 
  summarise(
    n_miss_dep_delay = sum(is.na(dep_delay)),
    n_miss_arr_delay = sum(is.na(arr_delay))
  )
```

    ## # A tibble: 16 x 3
    ##    carrier n_miss_dep_delay n_miss_arr_delay
    ##    <chr>              <int>            <int>
    ##  1 9E                  1044             1166
    ##  2 AA                   636              782
    ##  3 AS                     2                5
    ##  4 B6                   466              586
    ##  5 DL                   349              452
    ##  6 EV                  2817             3065
    ##  7 F9                     3                4
    ##  8 FL                    73               85
    ##  9 HA                     0                0
    ## 10 MQ                  1234             1360
    ## 11 OO                     3                3
    ## 12 UA                   686              883
    ## 13 US                   663              705
    ## 14 VX                    31               46
    ## 15 WN                   192              231
    ## 16 YV                    56               57

`mutate` observations
---------------------

Mutate adds new variables based on functions provided while preserving existing ones,

``` r
flights %>% 
  mutate(
    distance_k = distance / 1000,
    air_time_h = air_time / 60
  ) %>% 
  select(starts_with("distance"), starts_with("air_time"))
```

    ## # A tibble: 336,776 x 4
    ##    distance distance_k air_time air_time_h
    ##       <dbl>      <dbl>    <dbl>      <dbl>
    ##  1     1400      1.4        227      3.78 
    ##  2     1416      1.42       227      3.78 
    ##  3     1089      1.09       160      2.67 
    ##  4     1576      1.58       183      3.05 
    ##  5      762      0.762      116      1.93 
    ##  6      719      0.719      150      2.5  
    ##  7     1065      1.06       158      2.63 
    ##  8      229      0.229       53      0.883
    ##  9      944      0.944      140      2.33 
    ## 10      733      0.733      138      2.3  
    ## # ... with 336,766 more rows

Count observations with `n` and `count`
---------------------------------------

`n()` returns the total number of observation (in a group, if any).

``` r
flights %>% group_by(carrier) %>% summarise(n())
```

    ## # A tibble: 16 x 2
    ##    carrier `n()`
    ##    <chr>   <int>
    ##  1 9E      18460
    ##  2 AA      32729
    ##  3 AS        714
    ##  4 B6      54635
    ##  5 DL      48110
    ##  6 EV      54173
    ##  7 F9        685
    ##  8 FL       3260
    ##  9 HA        342
    ## 10 MQ      26397
    ## 11 OO         32
    ## 12 UA      58665
    ## 13 US      20536
    ## 14 VX       5162
    ## 15 WN      12275
    ## 16 YV        601

`tally` is short-hand for `summarise(n())`

``` r
flights %>% group_by(carrier) %>% tally()
```

    ## # A tibble: 16 x 2
    ##    carrier     n
    ##    <chr>   <int>
    ##  1 9E      18460
    ##  2 AA      32729
    ##  3 AS        714
    ##  4 B6      54635
    ##  5 DL      48110
    ##  6 EV      54173
    ##  7 F9        685
    ##  8 FL       3260
    ##  9 HA        342
    ## 10 MQ      26397
    ## 11 OO         32
    ## 12 UA      58665
    ## 13 US      20536
    ## 14 VX       5162
    ## 15 WN      12275
    ## 16 YV        601

and `count` is short-hand for `group_by(carrier) %>% tally() %>% ungroup()`

``` r
flights %>% count(carrier)
```

    ## # A tibble: 16 x 2
    ##    carrier     n
    ##    <chr>   <int>
    ##  1 9E      18460
    ##  2 AA      32729
    ##  3 AS        714
    ##  4 B6      54635
    ##  5 DL      48110
    ##  6 EV      54173
    ##  7 F9        685
    ##  8 FL       3260
    ##  9 HA        342
    ## 10 MQ      26397
    ## 11 OO         32
    ## 12 UA      58665
    ## 13 US      20536
    ## 14 VX       5162
    ## 15 WN      12275
    ## 16 YV        601

Nevertheless, `n()` with `sum` or `length` can be used for composing functions inside `mutate` or `summarise`:

what share of flights arrived late, for each airline?

``` r
flights %>% group_by(carrier) %>% summarise(sh_late_arr = sum(arr_delay > 0, na.rm = TRUE)/n() )
```

    ## # A tibble: 16 x 2
    ##    carrier sh_late_arr
    ##    <chr>         <dbl>
    ##  1 9E            0.360
    ##  2 AA            0.327
    ##  3 AS            0.265
    ##  4 B6            0.432
    ##  5 DL            0.341
    ##  6 EV            0.452
    ##  7 F9            0.572
    ##  8 FL            0.581
    ##  9 HA            0.284
    ## 10 MQ            0.443
    ## 11 OO            0.312
    ## 12 UA            0.379
    ## 13 US            0.358
    ## 14 VX            0.338
    ## 15 WN            0.432
    ## 16 YV            0.429

`arrange` to sort rows
----------------------

`arrange` sorts observations by lexicographic order of one or more variables. `desc` arranges in descending order

``` r
flights %>% count(carrier) %>% arrange(desc(n))
```

    ## # A tibble: 16 x 2
    ##    carrier     n
    ##    <chr>   <int>
    ##  1 UA      58665
    ##  2 B6      54635
    ##  3 EV      54173
    ##  4 DL      48110
    ##  5 AA      32729
    ##  6 MQ      26397
    ##  7 US      20536
    ##  8 9E      18460
    ##  9 WN      12275
    ## 10 VX       5162
    ## 11 FL       3260
    ## 12 AS        714
    ## 13 F9        685
    ## 14 YV        601
    ## 15 HA        342
    ## 16 OO         32

`top_n` sorts and returns the top n entries by value

``` r
flights %>% top_n(3, arr_delay)
```

    ## # A tibble: 3 x 19
    ##    year month   day dep_time sched_dep_time dep_delay arr_time
    ##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ## 1  2013     1     9      641            900      1301     1242
    ## 2  2013     1    10     1121           1635      1126     1239
    ## 3  2013     6    15     1432           1935      1137     1607
    ## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
    ## #   time_hour <dttm>

Keep unique rows with `distinct`
--------------------------------

`distinct` finds unique combinations of *rows in tibbles*, while `unique` finds unique *elements in vectors*

What are the destination from each airport?

``` r
flights %>% distinct(origin, dest)
```

    ## # A tibble: 224 x 2
    ##    origin dest 
    ##    <chr>  <chr>
    ##  1 EWR    IAH  
    ##  2 LGA    IAH  
    ##  3 JFK    MIA  
    ##  4 JFK    BQN  
    ##  5 LGA    ATL  
    ##  6 EWR    ORD  
    ##  7 EWR    FLL  
    ##  8 LGA    IAD  
    ##  9 JFK    MCO  
    ## 10 LGA    ORD  
    ## # ... with 214 more rows

Keep *all columns* with unique combinations of (origin, dest). Notice that this keeps the **first** observation of duplicated columns:

``` r
flights %>% distinct(origin, dest, .keep_all = TRUE)
```

    ## # A tibble: 224 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 214 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

`join` (merge) tibbles by value
-------------------------------

`airlines` in `nycflights13` contains the full names of airlines, reported as `carrier`in flights

``` r
data("airlines")
airlines
```

    ## # A tibble: 16 x 2
    ##    carrier name                       
    ##    <chr>   <chr>                      
    ##  1 9E      Endeavor Air Inc.          
    ##  2 AA      American Airlines Inc.     
    ##  3 AS      Alaska Airlines Inc.       
    ##  4 B6      JetBlue Airways            
    ##  5 DL      Delta Air Lines Inc.       
    ##  6 EV      ExpressJet Airlines Inc.   
    ##  7 F9      Frontier Airlines Inc.     
    ##  8 FL      AirTran Airways Corporation
    ##  9 HA      Hawaiian Airlines Inc.     
    ## 10 MQ      Envoy Air                  
    ## 11 OO      SkyWest Airlines Inc.      
    ## 12 UA      United Air Lines Inc.      
    ## 13 US      US Airways Inc.            
    ## 14 VX      Virgin America             
    ## 15 WN      Southwest Airlines Co.     
    ## 16 YV      Mesa Airlines Inc.

Do `airlines` and `flights` have variables in common

``` r
names(flights)
```

    ##  [1] "year"           "month"          "day"            "dep_time"      
    ##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
    ##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
    ## [13] "origin"         "dest"           "air_time"       "distance"      
    ## [17] "hour"           "minute"         "time_hour"

``` r
names(airlines)
```

    ## [1] "carrier" "name"

``` r
intersect(names(flights), names(airlines))
```

    ## [1] "carrier"

What variables are in `airlines` but not in `flights`?

``` r
setdiff(names(airlines), names(flights))
```

    ## [1] "name"

They have `carrier` is in common. Does it have common values between tibbles?

``` r
airlines %>% pull(carrier) %>% unique()
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

``` r
flights %>% pull(carrier) %>% unique()
```

    ##  [1] "UA" "AA" "B6" "DL" "EV" "MQ" "US" "WN" "VX" "FL" "AS" "9E" "F9" "HA"
    ## [15] "YV" "OO"

``` r
intersect(
  airlines %>% pull(carrier) %>% unique(),
  flights %>% pull(carrier) %>% unique()
  )
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

Then we can join the tibbles, to add `name` (full carrier name) from `airlines` to `flights`.

`left_join(x, y, by)` return all rows from x where there are matching values in y, and all columns from x and y. If there are multiple matches between x and y, all combination of the matches are returned.

See also `right_join`, `full_join`, `inner_join`, `anti_join`... we use `select(new_name = name)` to rename variables on the spot.

``` r
left_join(flights, airlines, by = "carrier") %>% 
  select(call_sign = carrier, carrier_name = name)
```

    ## # A tibble: 336,776 x 2
    ##    call_sign carrier_name            
    ##    <chr>     <chr>                   
    ##  1 UA        United Air Lines Inc.   
    ##  2 UA        United Air Lines Inc.   
    ##  3 AA        American Airlines Inc.  
    ##  4 B6        JetBlue Airways         
    ##  5 DL        Delta Air Lines Inc.    
    ##  6 UA        United Air Lines Inc.   
    ##  7 B6        JetBlue Airways         
    ##  8 EV        ExpressJet Airlines Inc.
    ##  9 B6        JetBlue Airways         
    ## 10 AA        American Airlines Inc.  
    ## # ... with 336,766 more rows

Did we miss anything? Compare results with `anti_join`

``` r
anti_join(airlines, flights, by = "carrier")
```

    ## # A tibble: 0 x 2
    ## # ... with 2 variables: carrier <chr>, name <chr>

Let's add a ficticious "SA" "Sant'Anna" airline and see:

``` r
airlines_sa <- airlines %>%
  add_row(carrier = "SA", name = "Sant'Anna Airlines")
```

``` r
anti_join(airlines_sa, flights, by = "carrier")
```

    ## # A tibble: 1 x 2
    ##   carrier name              
    ##   <chr>   <chr>             
    ## 1 SA      Sant'Anna Airlines

Variable types
--------------

``` r
flights %>% glimpse()
```

    ## Observations: 336,776
    ## Variables: 19
    ## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,...
    ## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 55...
    ## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 60...
    ## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2...
    ## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 7...
    ## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 7...
    ## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -...
    ## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV",...
    ## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79...
    ## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN...
    ## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR"...
    ## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL"...
    ## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138...
    ## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 94...
    ## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5,...
    ## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, ...
    ## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013...

Return variable types with typeof

``` r
flights %>% pull(dep_time) %>% typeof()
```

    ## [1] "integer"

``` r
flights %>% pull(dep_delay) %>% typeof()
```

    ## [1] "double"

``` r
flights %>% pull(carrier) %>% typeof()
```

    ## [1] "character"

``` r
flights %>% pull(time_hour) %>% typeof()
```

    ## [1] "double"

What are object types are there in R?

``` r
typeof(1)
```

    ## [1] "double"

``` r
typeof(1.0)
```

    ## [1] "double"

``` r
typeof(1L)
```

    ## [1] "integer"

``` r
typeof(c(1,2))
```

    ## [1] "double"

``` r
typeof(c("a","b"))
```

    ## [1] "character"

``` r
typeof(c("1","2"))
```

    ## [1] "character"

``` r
typeof(c(TRUE,FALSE))
```

    ## [1] "logical"

``` r
typeof(NA)
```

    ## [1] "logical"

``` r
typeof(c(1,2) == 1 )
```

    ## [1] "logical"

Factors
-------

objects of type `factor` are convenient to work with categorical values. We can transform (typically `character`) objects with `factor`

``` r
flights %>% pull(carrier)
```

    ##   [1] "UA" "UA" "AA" "B6" "DL" "UA" "B6" "EV" "B6" "AA" "B6" "B6" "UA" "UA"
    ##  [15] "AA" "B6" "UA" "B6" "MQ" "B6" "DL" "MQ" "AA" "DL" "UA" "MQ" "UA" "B6"
    ##  [29] "B6" "DL" "US" "AA" "UA" "EV" "MQ" "US" "AA" "UA" "AA" "WN" "US" "EV"
    ##  [43] "AA" "B6" "B6" "UA" "US" "UA" "B6" "UA" "UA" "B6" "B6" "DL" "DL" "DL"
    ##  [57] "DL" "AA" "AA" "MQ" "UA" "DL" "DL" "VX" "AA" "B6" "DL" "UA" "UA" "B6"
    ##  [71] "UA" "B6" "AA" "UA" "FL" "B6" "UA" "AA" "AS" "AA" "UA" "UA" "VX" "B6"
    ##  [85] "B6" "UA" "B6" "B6" "AA" "UA" "B6" "AA" "B6" "DL" "AA" "UA" "MQ" "DL"
    ##  [99] "UA" "US" "AA" "DL" "WN" "B6" "DL" "DL" "MQ" "B6" "AA" "UA" "DL" "B6"
    ## [113] "B6" "MQ" "DL" "EV" "9E" "DL" "EV" "MQ" "US" "EV" "DL" "FL" "B6" "B6"
    ## [127] "DL" "DL" "B6" "MQ" "EV" "US" "UA" "AA" "B6" "AA" "UA" "B6" "UA" "UA"
    ## [141] "UA" "AA" "MQ" "EV" "MQ" "F9" "AA" "MQ" "AA" "DL" "B6" "MQ" "UA" "EV"
    ## [155] "DL" "UA" "WN" "B6" "DL" "AA" "DL" "UA" "HA" "DL" "DL" "UA" "MQ" "DL"
    ## [169] "VX" "UA" "UA" "MQ" "UA" "B6" "UA" "B6" "US" "UA" "AA" "AA" "UA" "UA"
    ## [183] "AA" "UA" "AA" "B6" "B6" "B6" "MQ" "DL" "B6" "B6" "B6" "UA" "DL" "EV"
    ## [197] "WN" "UA" "B6" "UA" "VX" "B6" "B6" "WN" "DL" "DL" "B6" "WN" "AA" "MQ"
    ## [211] "B6" "EV" "B6" "EV" "MQ" "UA" "US" "DL" "UA" "DL" "US" "B6" "US" "UA"
    ## [225] "MQ" "DL" "US" "US" "EV" "DL" "FL" "EV" "MQ" "AA" "UA" "AA" "UA" "AA"
    ## [239] "EV" "VX" "UA" "EV" "UA" "AA" "UA" "B6" "EV" "UA" "UA" "AA" "DL" "MQ"
    ## [253] "B6" "DL" "EV" "DL" "US" "WN" "MQ" "UA" "B6" "DL" "UA" "MQ" "AA" "B6"
    ## [267] "UA" "DL" "UA" "EV" "WN" "UA" "B6" "DL" "US" "EV" "UA" "UA" "UA" "AA"
    ## [281] "DL" "MQ" "B6" "VX" "AA" "DL" "UA" "EV" "FL" "EV" "EV" "B6" "DL" "B6"
    ## [295] "MQ" "AA" "DL" "DL" "MQ" "EV" "MQ" "UA" "AA" "WN" "UA" "US" "EV" "UA"
    ## [309] "EV" "VX" "B6" "UA" "EV" "B6" "EV" "MQ" "UA" "AA" "DL" "WN" "EV" "B6"
    ## [323] "UA" "EV" "DL" "UA" "AA" "WN" "EV" "AA" "MQ" "EV" "DL" "DL" "B6" "UA"
    ## [337] "B6" "AA" "UA" "DL" "WN" "MQ" "US" "US" "B6" "MQ" "FL" "AA" "AA" "MQ"
    ## [351] "UA" "B6" "UA" "EV" "B6" "MQ" "AA" "WN" "B6" "US" "EV" "EV" "MQ" "EV"
    ## [365] "B6" "UA" "DL" "DL" "VX" "UA" "EV" "B6" "EV" "B6" "AA" "B6" "AA" "EV"
    ## [379] "AA" "UA" "WN" "EV" "B6" "EV" "EV" "EV" "DL" "EV" "B6" "WN" "MQ" "UA"
    ## [393] "UA" "UA" "US" "EV" "DL" "EV" "FL" "B6" "UA" "UA" "MQ" "B6" "B6" "DL"
    ## [407] "MQ" "UA" "EV" "EV" "EV" "B6" "UA" "UA" "B6" "UA" "DL" "DL" "DL" "DL"
    ## [421] "AA" "EV" "AA" "MQ" "AA" "US" "MQ" "9E" "9E" "B6" "MQ" "US" "EV" "9E"
    ## [435] "DL" "B6" "B6" "DL" "UA" "UA" "UA" "US" "MQ" "EV" "UA" "B6" "UA" "EV"
    ## [449] "MQ" "AA" "UA" "9E" "MQ" "UA" "B6" "DL" "DL" "B6" "EV" "MQ" "B6" "UA"
    ## [463] "AA" "MQ" "UA" "DL" "MQ" "UA" "UA" "B6" "B6" "MQ" "WN" "AA" "B6" "B6"
    ## [477] "UA" "EV" "AA" "UA" "US" "9E" "EV" "EV" "UA" "EV" "WN" "DL" "AA" "AA"
    ## [491] "UA" "B6" "DL" "DL" "UA" "9E" "DL" "MQ" "EV" "UA" "9E" "EV" "FL" "9E"
    ## [505] "AA" "9E" "DL" "MQ" "EV" "DL" "UA" "EV" "EV" "B6" "DL" "9E" "UA" "DL"
    ## [519] "EV" "B6" "WN" "MQ" "UA" "MQ" "AA" "B6" "UA" "AA" "AA" "B6" "DL" "DL"
    ## [533] "DL" "UA" "EV" "MQ" "UA" "DL" "US" "AA" "B6" "DL" "B6" "VX" "EV" "DL"
    ## [547] "EV" "B6" "EV" "US" "UA" "WN" "MQ" "UA" "UA" "B6" "9E" "EV" "MQ" "AA"
    ## [561] "UA" "EV" "EV" "B6" "B6" "AA" "DL" "EV" "DL" "EV" "AA" "DL" "VX" "AA"
    ## [575] "WN" "UA" "MQ" "AA" "UA" "UA" "AA" "US" "DL" "UA" "WN" "EV" "B6" "B6"
    ## [589] "UA" "UA" "B6" "AA" "F9" "B6" "UA" "AA" "B6" "MQ" "DL" "US" "UA" "AA"
    ## [603] "UA" "AA" "EV" "UA" "FL" "B6" "UA" "EV" "B6" "B6" "DL" "DL" "DL" "MQ"
    ## [617] "DL" "9E" "B6" "B6" "DL" "WN" "B6" "UA" "B6" "WN" "B6" "UA" "EV" "DL"
    ## [631] "B6" "B6" "UA" "EV" "B6" "UA" "DL" "UA" "EV" "MQ" "US" "UA" "MQ" "UA"
    ## [645] "AS" "B6" "UA" "EV" "B6" "EV" "WN" "MQ" "UA" "AA" "AA" "DL" "AA" "9E"
    ## [659] "US" "AA" "DL" "UA" "EV" "UA" "EV" "9E" "UA" "MQ" "UA" "EV" "B6" "MQ"
    ## [673] "UA" "EV" "UA" "AA" "DL" "DL" "AA" "AA" "AA" "FL" "EV" "9E" "VX" "US"
    ## [687] "MQ" "DL" "UA" "AA" "B6" "DL" "WN" "EV" "DL" "B6" "DL" "UA" "DL" "DL"
    ## [701] "B6" "DL" "EV" "9E" "US" "MQ" "DL" "UA" "DL" "UA" "AA" "EV" "DL" "EV"
    ## [715] "B6" "EV" "DL" "AA" "9E" "UA" "DL" "MQ" "EV" "AA" "EV" "9E" "AA" "UA"
    ## [729] "B6" "MQ" "9E" "EV" "B6" "EV" "VX" "UA" "9E" "9E" "B6" "UA" "DL" "UA"
    ## [743] "EV" "9E" "AA" "UA" "EV" "UA" "MQ" "MQ" "EV" "UA" "AA" "9E" "EV" "MQ"
    ## [757] "9E" "B6" "UA" "FL" "B6" "9E" "B6" "DL" "UA" "EV" "B6" "WN" "EV" "AA"
    ## [771] "B6" "B6" "UA" "UA" "UA" "EV" "B6" "9E" "UA" "MQ" "B6" "B6" "MQ" "UA"
    ## [785] "EV" "EV" "B6" "MQ" "MQ" "EV" "WN" "UA" "MQ" "B6" "UA" "DL" "B6" "UA"
    ## [799] "B6" "MQ" "EV" "9E" "EV" "EV" "B6" "B6" "MQ" "AA" "MQ" "B6" "UA" "B6"
    ## [813] "B6" "B6" "EV" "AA" "B6" "B6" "B6" "B6" "B6" "EV" "EV" "B6" "B6" "B6"
    ## [827] "EV" "B6" "B6" "B6" "EV" "EV" "B6" "B6" "EV" "B6" "B6" "B6" "EV" "AA"
    ## [841] "AA" "B6" "B6" "B6" "US" "UA" "AA" "UA" "B6" "B6" "B6" "B6" "AA" "B6"
    ## [855] "DL" "EV" "DL" "DL" "FL" "UA" "UA" "UA" "EV" "EV" "9E" "B6" "WN" "MQ"
    ## [869] "UA" "US" "AA" "UA" "UA" "DL" "DL" "AA" "B6" "EV" "DL" "WN" "B6" "B6"
    ## [883] "UA" "US" "AA" "MQ" "MQ" "MQ" "UA" "UA" "US" "DL" "WN" "EV" "EV" "US"
    ## [897] "B6" "DL" "WN" "EV" "UA" "AA" "UA" "UA" "EV" "US" "UA" "B6" "UA" "EV"
    ## [911] "AA" "B6" "B6" "US" "UA" "UA" "US" "DL" "UA" "DL" "UA" "AA" "B6" "DL"
    ## [925] "DL" "DL" "B6" "MQ" "US" "VX" "EV" "AA" "AA" "DL" "UA" "B6" "DL" "UA"
    ## [939] "AA" "MQ" "AA" "B6" "DL" "UA" "AA" "B6" "UA" "UA" "MQ" "AS" "UA" "VX"
    ## [953] "UA" "UA" "FL" "B6" "DL" "B6" "AA" "B6" "UA" "B6" "B6" "WN" "UA" "B6"
    ## [967] "AA" "AA" "UA" "WN" "EV" "UA" "9E" "DL" "AA" "UA" "B6" "UA" "9E" "EV"
    ## [981] "EV" "UA" "EV" "DL" "B6" "B6" "DL" "DL" "US" "AA" "B6" "DL" "AA" "MQ"
    ## [995] "UA" "AA" "DL" "DL" "US"
    ##  [ reached getOption("max.print") -- omitted 335777 entries ]

``` r
carriers <- flights %>% pull(carrier) %>% factor()

levels(carriers)
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

``` r
flights %>% pull(carrier) %>% sort() %>% unique()
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

manually set factor levels:

``` r
c("a", "b") %>% factor(levels = c("a", "b"))
```

    ## [1] a b
    ## Levels: a b

``` r
c("a", "b") %>% factor(levels = c("a", "b", "c"))
```

    ## [1] a b
    ## Levels: a b c

``` r
c("a", "b", "z") %>% factor(levels = c("a", "b", "c"))
```

    ## [1] a    b    <NA>
    ## Levels: a b c

assign meaningful labels to factor levels:

``` r
c("a", "b") %>% factor()
```

    ## [1] a b
    ## Levels: a b

``` r
c("a", "b") %>% factor(labels = c("alpha", "beta"))
```

    ## [1] alpha beta 
    ## Levels: alpha beta

work within `flights` tibble to change `carrier` to factor:

``` r
flights %>% mutate(carrier = factor(carrier))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <fct>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

since airlines uniquely maps carrier codes in airline names, we can use that to set factor levels

``` r
flights %>%
  mutate(
    carrier = factor(
      carrier,
      levels = airlines %>% pull(carrier), 
      labels = airlines %>% pull(name)
    )
  ) %>% 
  select(year:day, carrier)
```

    ## # A tibble: 336,776 x 4
    ##     year month   day carrier                 
    ##    <int> <int> <int> <fct>                   
    ##  1  2013     1     1 United Air Lines Inc.   
    ##  2  2013     1     1 United Air Lines Inc.   
    ##  3  2013     1     1 American Airlines Inc.  
    ##  4  2013     1     1 JetBlue Airways         
    ##  5  2013     1     1 Delta Air Lines Inc.    
    ##  6  2013     1     1 United Air Lines Inc.   
    ##  7  2013     1     1 JetBlue Airways         
    ##  8  2013     1     1 ExpressJet Airlines Inc.
    ##  9  2013     1     1 JetBlue Airways         
    ## 10  2013     1     1 American Airlines Inc.  
    ## # ... with 336,766 more rows

in shorhand:

``` r
flights %>%
  mutate(carrier = factor(carrier, levels = airlines$carrier, labels = airlines$name))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <fct>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

Data input and output
---------------------

Import a table with `read_csv` (NB, different than `read.csv`)

``` r
flights_import <- read_csv("./data/flights.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   year = col_integer(),
    ##   month = col_integer(),
    ##   day = col_integer(),
    ##   dep_time = col_integer(),
    ##   sched_dep_time = col_integer(),
    ##   dep_delay = col_integer(),
    ##   arr_time = col_integer(),
    ##   sched_arr_time = col_integer(),
    ##   arr_delay = col_integer(),
    ##   carrier = col_character(),
    ##   flight = col_integer(),
    ##   tailnum = col_character(),
    ##   origin = col_character(),
    ##   dest = col_character(),
    ##   air_time = col_integer(),
    ##   distance = col_integer(),
    ##   hour = col_integer(),
    ##   minute = col_integer(),
    ##   time_hour = col_datetime(format = "")
    ## )

``` r
glimpse(flights_import)
```

    ## Observations: 100
    ## Variables: 19
    ## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,...
    ## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 55...
    ## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 60...
    ## $ dep_delay      <int> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2...
    ## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 7...
    ## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 7...
    ## $ arr_delay      <int> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -...
    ## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV",...
    ## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79...
    ## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN...
    ## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR"...
    ## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL"...
    ## $ air_time       <int> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138...
    ## $ distance       <int> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 94...
    ## $ hour           <int> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5,...
    ## $ minute         <int> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, ...
    ## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013...

``` r
challenge <- read_csv("./data/challenge.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   x = col_integer(),
    ##   y = col_character()
    ## )

    ## Warning in rbind(names(probs), probs_f): number of columns of result is not
    ## a multiple of vector length (arg 1)

    ## Warning: 1000 parsing failures.
    ## row # A tibble: 5 x 5 col     row col   expected               actual             file               expected   <int> <chr> <chr>                  <chr>              <chr>              actual 1  1001 x     no trailing characters .23837975086644292 './data/challenge~ file 2  1002 x     no trailing characters .41167997173033655 './data/challenge~ row 3  1003 x     no trailing characters .7460716762579978  './data/challenge~ col 4  1004 x     no trailing characters .723450553836301   './data/challenge~ expected 5  1005 x     no trailing characters .614524137461558   './data/challenge~
    ## ... ................. ... .......................................................................... ........ .......................................................................... ...... .......................................................................... .... .......................................................................... ... .......................................................................... ... .......................................................................... ........ ..........................................................................
    ## See problems(...) for more details.

what's wrong? let's inspect:

``` r
problems(challenge)
```

    ## # A tibble: 1,000 x 5
    ##      row col   expected               actual             file             
    ##    <int> <chr> <chr>                  <chr>              <chr>            
    ##  1  1001 x     no trailing characters .23837975086644292 './data/challeng~
    ##  2  1002 x     no trailing characters .41167997173033655 './data/challeng~
    ##  3  1003 x     no trailing characters .7460716762579978  './data/challeng~
    ##  4  1004 x     no trailing characters .723450553836301   './data/challeng~
    ##  5  1005 x     no trailing characters .614524137461558   './data/challeng~
    ##  6  1006 x     no trailing characters .473980569280684   './data/challeng~
    ##  7  1007 x     no trailing characters .5784610391128808  './data/challeng~
    ##  8  1008 x     no trailing characters .2415937229525298  './data/challeng~
    ##  9  1009 x     no trailing characters .11437866208143532 './data/challeng~
    ## 10  1010 x     no trailing characters .2983446326106787  './data/challeng~
    ## # ... with 990 more rows

``` r
challenge <- read_csv(readr_example("challenge.csv"), guess_max = 1500)
```

    ## Parsed with column specification:
    ## cols(
    ##   x = col_double(),
    ##   y = col_date(format = "")
    ## )

`readr` tries to guess the type of object based on heuristics:

``` r
guess_parser("1,234")
```

    ## [1] "number"

``` r
guess_parser(c(".", "-"))
```

    ## [1] "character"

``` r
guess_parser(c("10W", "20N"))
```

    ## [1] "character"

``` r
guess_parser("10:30")
```

    ## [1] "time"
