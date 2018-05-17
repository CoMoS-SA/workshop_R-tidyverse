Data transformation
================
Matteo Sostero

Install required packages
-------------------------

We need `tidyverse` and related dependencies, and example data provided by`nycflights13`.

`CTRL/CMD + ENTER` to run the block of code below:

Load the packages for this session
----------------------------------

`tidyverse` loads (eight) packages of the *tidyverse* and shows their version. The *nycflights13* package contains different example datasets, including *flights*

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.4
    ## v tibble  1.4.2     v dplyr   0.7.4
    ## v tidyr   0.8.0     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts ------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(nycflights13)
```

Load example data
-----------------

load the `flights` dataset from `nycflights13`

``` r
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
flights %>% filter(month %in% c(2,4))
```

    ## # A tibble: 53,281 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     2     1      456            500        -4      652
    ##  2  2013     2     1      520            525        -5      816
    ##  3  2013     2     1      527            530        -3      837
    ##  4  2013     2     1      532            540        -8     1007
    ##  5  2013     2     1      540            540         0      859
    ##  6  2013     2     1      552            600        -8      714
    ##  7  2013     2     1      552            600        -8      919
    ##  8  2013     2     1      552            600        -8      655
    ##  9  2013     2     1      553            600        -7      833
    ## 10  2013     2     1      553            600        -7      821
    ## # ... with 53,271 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

`select` and `pull` variables
-----------------------------

We can select columns by name; the result is always a tibble. Pressing TAB with the cursorinside `select( )` provides variable name completion.

``` r
flights %>% select(year, month, day, dep_time, dep_delay)
```

    ## # A tibble: 336,776 x 5
    ##     year month   day dep_time dep_delay
    ##    <int> <int> <int>    <int>     <dbl>
    ##  1  2013     1     1      517         2
    ##  2  2013     1     1      533         4
    ##  3  2013     1     1      542         2
    ##  4  2013     1     1      544        -1
    ##  5  2013     1     1      554        -6
    ##  6  2013     1     1      554        -4
    ##  7  2013     1     1      555        -5
    ##  8  2013     1     1      557        -3
    ##  9  2013     1     1      557        -3
    ## 10  2013     1     1      558        -2
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

    ##  [1] "UA" "UA" "AA" "B6" "DL" "UA" "B6" "EV" "B6" "AA" "B6" "B6" "UA" "UA"
    ## [15] "AA" "B6" "UA" "B6" "MQ" "B6"
    ##  [ reached getOption("max.print") -- omitted 336756 entries ]

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
    avg_dep_delay = mean(dep_delay, na.rm = TRUE),
    avg_arr_delay = mean(arr_delay, na.rm = TRUE)
  )
```

    ## # A tibble: 16 x 3
    ##    carrier avg_dep_delay avg_arr_delay
    ##    <chr>           <dbl>         <dbl>
    ##  1 9E              16.7          7.38 
    ##  2 AA               8.59         0.364
    ##  3 AS               5.80        -9.93 
    ##  4 B6              13.0          9.46 
    ##  5 DL               9.26         1.64 
    ##  6 EV              20.0         15.8  
    ##  7 F9              20.2         21.9  
    ##  8 FL              18.7         20.1  
    ##  9 HA               4.90        -6.92 
    ## 10 MQ              10.6         10.8  
    ## 11 OO              12.6         11.9  
    ## 12 UA              12.1          3.56 
    ## 13 US               3.78         2.13 
    ## 14 VX              12.9          1.76 
    ## 15 WN              17.7          9.65 
    ## 16 YV              19.0         15.6

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
flights %>% group_by(carrier) %>% summarise(total_obs = n())
```

    ## # A tibble: 16 x 2
    ##    carrier total_obs
    ##    <chr>       <int>
    ##  1 9E          18460
    ##  2 AA          32729
    ##  3 AS            714
    ##  4 B6          54635
    ##  5 DL          48110
    ##  6 EV          54173
    ##  7 F9            685
    ##  8 FL           3260
    ##  9 HA            342
    ## 10 MQ          26397
    ## 11 OO             32
    ## 12 UA          58665
    ## 13 US          20536
    ## 14 VX           5162
    ## 15 WN          12275
    ## 16 YV            601

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

``` r
flights %>% count(carrier, dest) 
```

    ## # A tibble: 314 x 3
    ##    carrier dest      n
    ##    <chr>   <chr> <int>
    ##  1 9E      ATL      59
    ##  2 9E      AUS       2
    ##  3 9E      AVL      10
    ##  4 9E      BGR       1
    ##  5 9E      BNA     474
    ##  6 9E      BOS     914
    ##  7 9E      BTV       2
    ##  8 9E      BUF     833
    ##  9 9E      BWI     856
    ## 10 9E      CAE       3
    ## # ... with 304 more rows

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
flights %>% top_n(10, arr_delay)
```

    ## # A tibble: 10 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     9      641            900      1301     1242
    ##  2  2013     1    10     1121           1635      1126     1239
    ##  3  2013    12     5      756           1700       896     1058
    ##  4  2013     3    17     2321            810       911      135
    ##  5  2013     4    10     1100           1900       960     1342
    ##  6  2013     5     3     1133           2055       878     1250
    ##  7  2013     6    15     1432           1935      1137     1607
    ##  8  2013     7    22      845           1600      1005     1044
    ##  9  2013     7    22     2257            759       898      121
    ## 10  2013     9    20     1139           1845      1014     1457
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

What variables are in `airlines` but not in `flights` (and viceversa)?

``` r
setdiff(names(airlines), names(flights))
```

    ## [1] "name"

``` r
setdiff(names(flights), names(airlines))
```

    ##  [1] "year"           "month"          "day"            "dep_time"      
    ##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
    ##  [9] "arr_delay"      "flight"         "tailnum"        "origin"        
    ## [13] "dest"           "air_time"       "distance"       "hour"          
    ## [17] "minute"         "time_hour"

They have `carrier` is in common. Does it have common values between tibbles?

``` r
airlines %>% pull(carrier) %>% unique() %>% sort()
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

``` r
flights %>% pull(carrier) %>% unique() %>% sort()
```

    ##  [1] "9E" "AA" "AS" "B6" "DL" "EV" "F9" "FL" "HA" "MQ" "OO" "UA" "US" "VX"
    ## [15] "WN" "YV"

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

anti_join(airlines_sa, flights, by = "carrier")
```

    ## # A tibble: 1 x 2
    ##   carrier name              
    ##   <chr>   <chr>             
    ## 1 SA      Sant'Anna Airlines

Variable types
--------------

`glimpse` shows all variable names and `<types>`, including:

-   `<int>` **integer**: *signed* (positive or negative) integer
-   `<dbl>` **double**: "double-precision" real number
-   `<chr>` **character**: character string
-   `<fct>` **factor**: categorical variable
-   `<dttm>` **date-time**

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

Inspect variable types with typeof:

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
# Numbers are doubles by default…
typeof(1.0)
```

    ## [1] "double"

``` r
typeof(1)
```

    ## [1] "double"

``` r
# …unless specified as integers with `L` or coerced
typeof(1L)
```

    ## [1] "integer"

``` r
as.integer(1) %>% typeof()
```

    ## [1] "integer"

``` r
# strings:
typeof("a")
```

    ## [1] "character"

*atomic vector* and *list* classes
----------------------------------

The main type of *R* objects are *vectors*, either:

1.  **lists**: (heterogeneous) contain elements of different type;
2.  **atomic vectors**: contain elements of same type:
    1.  *numeric*: *integer* or *double*
    2.  *character*
    3.  *logical*
    4.  *complex*
    5.  *raw*

We can construct **atomic vectors** by *concatenating* `,`-sepatated elements with `c( )`

Atomic vectors:

``` r
# numeric double
typeof(c(1, 2, 3))
```

    ## [1] "double"

``` r
# numeric integer
typeof(c(1L, 2L, 3L))
```

    ## [1] "integer"

``` r
# …character…
typeof(c("a","b"))
```

    ## [1] "character"

``` r
typeof(c("1","2"))
```

    ## [1] "character"

``` r
# …logical…
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

We can initialise empty **lists** of lenght *n* with `vector("list", n)` and assign elements by positions

``` r
ex_list <- vector("list", 4) # initialise list

ex_list # empty list
```

    ## [[1]]
    ## NULL
    ## 
    ## [[2]]
    ## NULL
    ## 
    ## [[3]]
    ## NULL
    ## 
    ## [[4]]
    ## NULL

``` r
# assign elements to list by position:
ex_list[[1]] <- 10L # a lonely integer in the 1st slot
ex_list[[2]] <- c("a", "b") # an atomic character vector in 2nd slot
ex_list[[3]] <- c(1.1, 2.2) # an atomic double vector in 3rd slot
ex_list[[4]] <- c(NA, TRUE, FALSE) # an atomic logical vector in 3rd slot

ex_list # populated list
```

    ## [[1]]
    ## [1] 10
    ## 
    ## [[2]]
    ## [1] "a" "b"
    ## 
    ## [[3]]
    ## [1] 1.1 2.2
    ## 
    ## [[4]]
    ## [1]    NA  TRUE FALSE

Factors
-------

`factor` variables are convenient to work with categorical values. We can transform (typically `character`) objects with `factor`

``` r
flights %>%
  pull(carrier) %>%
  head(n = 10) # show only first 10 elements
```

    ##  [1] "UA" "UA" "AA" "B6" "DL" "UA" "B6" "EV" "B6" "AA"

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

``` r
typeof(carriers) # factors are stored as type integer
```

    ## [1] "integer"

We can manually set factor levels:

``` r
c("a", "b") %>% factor(levels = c("a", "b"))           # levels all observed in the vector
```

    ## [1] a b
    ## Levels: a b

``` r
c("a", "b") %>% factor(levels = c("a", "b", "c"))      # as before, and one more level
```

    ## [1] a b
    ## Levels: a b c

``` r
c("a", "b", "z") %>% factor(levels = c("a", "b", "c")) # levels in data are different
```

    ## [1] a    b    <NA>
    ## Levels: a b c

Assign meaningful labels to factor levels. By default, levels are *unique, sorted* values, unless we provide a custom order

``` r
c("a", "b") %>% factor() # by default, levels and labels are unique sorted values
```

    ## [1] a b
    ## Levels: a b

``` r
c("a", "b") %>% factor(levels = c("b", "a")) # custom level order
```

    ## [1] a b
    ## Levels: b a

We can change how levels are labelled by setting `labels` (in the same order as `levels`):

``` r
c("a", "b") %>% factor(labels = c("alpha", "beta")) # "a" = "alpha" and "b" = "beta"
```

    ## [1] alpha beta 
    ## Levels: alpha beta

``` r
c("a", "b") %>% factor(labels = c("beta", "alpha")) # mind the order! "a" = "beta" and "b" = "alpha"
```

    ## [1] beta  alpha
    ## Levels: beta alpha

``` r
# better carefully set both levels and labels:
c("a", "b") %>% factor(levels = c("b", "a"), labels = c("beta", "alpha")) 
```

    ## [1] alpha beta 
    ## Levels: beta alpha

Example: work within `flights` tibble to change `carrier` to factor:

``` r
flights %>%
  mutate(carrier = factor(carrier)) %>%
  select(year:day, carrier)
```

    ## # A tibble: 336,776 x 4
    ##     year month   day carrier
    ##    <int> <int> <int> <fct>  
    ##  1  2013     1     1 UA     
    ##  2  2013     1     1 UA     
    ##  3  2013     1     1 AA     
    ##  4  2013     1     1 B6     
    ##  5  2013     1     1 DL     
    ##  6  2013     1     1 UA     
    ##  7  2013     1     1 B6     
    ##  8  2013     1     1 EV     
    ##  9  2013     1     1 B6     
    ## 10  2013     1     1 AA     
    ## # ... with 336,766 more rows

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

in shorhand, using `$` to select a variable in a tibble

``` r
flights %>%
  mutate(carrier = factor(carrier, levels = airlines$carrier, labels = airlines$name)) %>% 
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

Date and time variables
-----------------------

Dates are generally difficult! `lubridate` package (in `tidyverse`, but not loaded automatically) makes it easier:

The functions `ymd()` `dmy()` etc., allow to parse strings containing "Year, Month, Date" values (in a given order)

``` r
library(lubridate) # installed with tidyverse, but not loaded by default
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following object is masked from 'package:base':
    ## 
    ##     date

``` r
ymd("2018-05-17") # parse date Y-M-D
```

    ## [1] "2018-05-17"

``` r
dmy("15/05/2018") # input date in different order…
```

    ## [1] "2018-05-15"

``` r
mdy("05.15.2018") # …and with different separators
```

    ## [1] "2018-05-15"

``` r
mdy("05.15.2018") == dmy("15/05/2018") # they are parsed to identical representations
```

    ## [1] TRUE

``` r
mdy("May 17th 2018")  # Can parse natural language
```

    ## [1] "2018-05-17"

``` r
dmy("17 Maggio 2018") # also in non-English other locales!
```

    ## [1] "2018-05-17"

``` r
# Parse heterogeneous formats (still Y-M-D), but written differently
c(20090101, "2009-01-02", "2009 01 03", "2009-1-4",
  "2009-1, 5", "Created on 2009 1 6", "200901 !!! 07") %>% ymd()
```

    ## [1] "2009-01-01" "2009-01-02" "2009-01-03" "2009-01-04" "2009-01-05"
    ## [6] "2009-01-06" "2009-01-07"

Operations with dates:

``` r
typeof(ymd("2018-05-17")) # actually a double number previewed in human-redable format
```

    ## [1] "double"

``` r
dmy("16/05/2018") > dmy("15/05/2018") # > means "after"
```

    ## [1] TRUE

Construct dates from separate columns:

``` r
flights %>% select(year, month, day) # separate year, month, day (integer) variables
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

``` r
flights %>% select(year, month, day) %>%
  unite(date, year, month, day, sep = "-") # paste variables together as (dash-separated) character
```

    ## # A tibble: 336,776 x 1
    ##    date    
    ##    <chr>   
    ##  1 2013-1-1
    ##  2 2013-1-1
    ##  3 2013-1-1
    ##  4 2013-1-1
    ##  5 2013-1-1
    ##  6 2013-1-1
    ##  7 2013-1-1
    ##  8 2013-1-1
    ##  9 2013-1-1
    ## 10 2013-1-1
    ## # ... with 336,766 more rows

``` r
flights %>% select(year, month, day) %>%
  unite(date, year, month, day, sep = "-") %>% 
  mutate(date = ymd(date))
```

    ## # A tibble: 336,776 x 1
    ##    date      
    ##    <date>    
    ##  1 2013-01-01
    ##  2 2013-01-01
    ##  3 2013-01-01
    ##  4 2013-01-01
    ##  5 2013-01-01
    ##  6 2013-01-01
    ##  7 2013-01-01
    ##  8 2013-01-01
    ##  9 2013-01-01
    ## 10 2013-01-01
    ## # ... with 336,766 more rows

What's in a date? Obviously *day*, *month*, *year*. But also time zone!

``` r
dmy("16/05-2018")
```

    ## [1] "2018-05-16"
