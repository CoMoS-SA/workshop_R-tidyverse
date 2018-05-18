Data types, lists, and mapping
================
Matteo Sostero

Packages for this session
-------------------------

| package       | purpose                          | installation               |
|---------------|----------------------------------|----------------------------|
| `tidyverse`   | everything                       | CRAN                       |
| `nycflight13` | example datasets                 | CRAN                       |
| `lubridate`   | working with dates               | installed with `tidyverse` |
| `glue`        | pasting and interpreting strings | installed with `tidyverse` |

If not yet installed, download packages with `install.packages("name")`. If asked, **do not compile from source**.

Load the packages for the session:

``` r
# `tidyverse` loads the core packages of the *tidyverse* and shows their version.
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
library(lubridate) # tidyverse, not loaded by default
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following object is masked from 'package:base':
    ## 
    ##     date

``` r
library(glue) # tidyverse, not loaded by default
```

    ## 
    ## Attaching package: 'glue'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     collapse

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

Vectors: *atomic vector* and *list* classes
-------------------------------------------

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
typeof(c("a", "b"))
```

    ## [1] "character"

``` r
typeof(c("1", "2"))
```

    ## [1] "character"

``` r
# …logical…
typeof(c(TRUE, FALSE))
```

    ## [1] "logical"

``` r
typeof(NA)
```

    ## [1] "logical"

``` r
typeof(c(1, 2) == 1)
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

Applying functions to vector (list) elements with `map`
-------------------------------------------------------

`map(.x, .f)` applies a function `.f` to every element of a list or atomic vector `.x` Functions can be:

-   already defined in R: `sum`, `mean`, `filter`, `mutate`, ecc.
-   defined in place as “anonymous functions” `.f` with the syntax `~ .`, where `~` introduces a function and `.` is the argument

``` r
# a list of three elements: 2, 4, and 6
list(2, 4, 6)
```

    ## [[1]]
    ## [1] 2
    ## 
    ## [[2]]
    ## [1] 4
    ## 
    ## [[3]]
    ## [1] 6

``` r
# every list element is actually a lenght-1 atomic vector

# we map the list elements .x to a function .f = ~ .^2
# the function is introduced by ~ and takes the argument . and raises ^ to the power of 2
map(.x = list(2, 4, 6), .f = ~ .^2)
```

    ## [[1]]
    ## [1] 4
    ## 
    ## [[2]]
    ## [1] 16
    ## 
    ## [[3]]
    ## [1] 36

``` r
# equivalent to piping the list as first argument of map(.)
# and omit the argument names .x and .f
list(2, 4, 6) %>% map(.f = ~ .^2)
```

    ## [[1]]
    ## [1] 4
    ## 
    ## [[2]]
    ## [1] 16
    ## 
    ## [[3]]
    ## [1] 36

we can map lists containing atomic vectors of different lenghts:

``` r
# A list of three elements, containing numeric vectors of different lenghts
list(c(1, 2), c(3, 4, 5, 6), c(7, 8, 9))
```

    ## [[1]]
    ## [1] 1 2
    ## 
    ## [[2]]
    ## [1] 3 4 5 6
    ## 
    ## [[3]]
    ## [1] 7 8 9

``` r
# we map functions that allow vector arguments, and returns a single element
list(c(1, 2), c(3, 4, 5, 6), c(7, 8, 9)) %>% map(~ sum(.))
```

    ## [[1]]
    ## [1] 3
    ## 
    ## [[2]]
    ## [1] 18
    ## 
    ## [[3]]
    ## [1] 24

``` r
list(c(1, 2), c(3, 4, 5, 6), c(7, 8, 9)) %>% map(~ mean(.))
```

    ## [[1]]
    ## [1] 1.5
    ## 
    ## [[2]]
    ## [1] 4.5
    ## 
    ## [[3]]
    ## [1] 8

we can map functions to list of string vectors as well. For instance, `collapse` takes a vector of character and pastes them together

``` r
list(c("a", "b", "c"), c("hello", "bye"))
```

    ## [[1]]
    ## [1] "a" "b" "c"
    ## 
    ## [[2]]
    ## [1] "hello" "bye"

``` r
list(c("a", "b", "c"), c("hello", "bye")) %>% map(~ collapse(.))
```

    ## [[1]]
    ## abc
    ## 
    ## [[2]]
    ## hellobye

`tibble` and `data.frame` objects are also `list`! Hence, we can `map` them:

``` r
is.list(flights) # the tibble is also a list
```

    ## [1] TRUE

``` r
length(flights) # a list of 19 elements (the variables, or columns)
```

    ## [1] 19

``` r
# let's take the first elements of the “list” flights:
flights[[1]]
```

    ##  [1] 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013
    ## [15] 2013 2013 2013 2013 2013 2013
    ##  [ reached getOption("max.print") -- omitted 336756 entries ]

``` r
# it's a numeric vector, with as many elements as observations (rows) of flights
```

We can `map` the variables that make up `flights`

``` r
# what is the type of each variable
flights %>% map(~ typeof(.))
```

    ## $year
    ## [1] "integer"
    ## 
    ## $month
    ## [1] "integer"
    ## 
    ## $day
    ## [1] "integer"
    ## 
    ## $dep_time
    ## [1] "integer"
    ## 
    ## $sched_dep_time
    ## [1] "integer"
    ## 
    ## $dep_delay
    ## [1] "double"
    ## 
    ## $arr_time
    ## [1] "integer"
    ## 
    ## $sched_arr_time
    ## [1] "integer"
    ## 
    ## $arr_delay
    ## [1] "double"
    ## 
    ## $carrier
    ## [1] "character"
    ## 
    ## $flight
    ## [1] "integer"
    ## 
    ## $tailnum
    ## [1] "character"
    ## 
    ## $origin
    ## [1] "character"
    ## 
    ## $dest
    ## [1] "character"
    ## 
    ## $air_time
    ## [1] "double"
    ## 
    ## $distance
    ## [1] "double"
    ## 
    ## $hour
    ## [1] "double"
    ## 
    ## $minute
    ## [1] "double"
    ## 
    ## $time_hour
    ## [1] "double"

``` r
# is each variable of type integer?
flights %>% map(~ is.integer(.))
```

    ## $year
    ## [1] TRUE
    ## 
    ## $month
    ## [1] TRUE
    ## 
    ## $day
    ## [1] TRUE
    ## 
    ## $dep_time
    ## [1] TRUE
    ## 
    ## $sched_dep_time
    ## [1] TRUE
    ## 
    ## $dep_delay
    ## [1] FALSE
    ## 
    ## $arr_time
    ## [1] TRUE
    ## 
    ## $sched_arr_time
    ## [1] TRUE
    ## 
    ## $arr_delay
    ## [1] FALSE
    ## 
    ## $carrier
    ## [1] FALSE
    ## 
    ## $flight
    ## [1] TRUE
    ## 
    ## $tailnum
    ## [1] FALSE
    ## 
    ## $origin
    ## [1] FALSE
    ## 
    ## $dest
    ## [1] FALSE
    ## 
    ## $air_time
    ## [1] FALSE
    ## 
    ## $distance
    ## [1] FALSE
    ## 
    ## $hour
    ## [1] FALSE
    ## 
    ## $minute
    ## [1] FALSE
    ## 
    ## $time_hour
    ## [1] FALSE

``` r
# find number of elements in each variable
flights %>% map(~ length(.))
```

    ## $year
    ## [1] 336776
    ## 
    ## $month
    ## [1] 336776
    ## 
    ## $day
    ## [1] 336776
    ## 
    ## $dep_time
    ## [1] 336776
    ## 
    ## $sched_dep_time
    ## [1] 336776
    ## 
    ## $dep_delay
    ## [1] 336776
    ## 
    ## $arr_time
    ## [1] 336776
    ## 
    ## $sched_arr_time
    ## [1] 336776
    ## 
    ## $arr_delay
    ## [1] 336776
    ## 
    ## $carrier
    ## [1] 336776
    ## 
    ## $flight
    ## [1] 336776
    ## 
    ## $tailnum
    ## [1] 336776
    ## 
    ## $origin
    ## [1] 336776
    ## 
    ## $dest
    ## [1] 336776
    ## 
    ## $air_time
    ## [1] 336776
    ## 
    ## $distance
    ## [1] 336776
    ## 
    ## $hour
    ## [1] 336776
    ## 
    ## $minute
    ## [1] 336776
    ## 
    ## $time_hour
    ## [1] 336776

``` r
# count missing elements in each variable
flights %>% map(~ sum(is.na(.)))
```

    ## $year
    ## [1] 0
    ## 
    ## $month
    ## [1] 0
    ## 
    ## $day
    ## [1] 0
    ## 
    ## $dep_time
    ## [1] 8255
    ## 
    ## $sched_dep_time
    ## [1] 0
    ## 
    ## $dep_delay
    ## [1] 8255
    ## 
    ## $arr_time
    ## [1] 8713
    ## 
    ## $sched_arr_time
    ## [1] 0
    ## 
    ## $arr_delay
    ## [1] 9430
    ## 
    ## $carrier
    ## [1] 0
    ## 
    ## $flight
    ## [1] 0
    ## 
    ## $tailnum
    ## [1] 2512
    ## 
    ## $origin
    ## [1] 0
    ## 
    ## $dest
    ## [1] 0
    ## 
    ## $air_time
    ## [1] 9430
    ## 
    ## $distance
    ## [1] 0
    ## 
    ## $hour
    ## [1] 0
    ## 
    ## $minute
    ## [1] 0
    ## 
    ## $time_hour
    ## [1] 0

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
c("a", "b") %>% factor(levels = c("a", "b")) # levels all observed in the vector
```

    ## [1] a b
    ## Levels: a b

``` r
c("a", "b") %>% factor(levels = c("a", "b", "c")) # as before, and one more level
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
mdy("May 17th 2018") # Can parse natural language
```

    ## [1] "2018-05-17"

``` r
dmy("17 Maggio 2018") # also in non-English other locales!
```

    ## [1] "2018-05-17"

``` r
# Parse heterogeneous formats (still Y-M-D), but written differently
c(
  20090101, "2009-01-02", "2009 01 03", "2009-1-4",
  "2009-1, 5", "Created on 2009 1 6", "200901 !!! 07"
) %>% ymd()
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

``` r
today() # current date
```

    ## [1] "2018-05-18"

``` r
# extract components:
today() %>% day()
```

    ## [1] 18

``` r
today() %>% month()
```

    ## [1] 5

``` r
today() %>% quarter()
```

    ## [1] 2

``` r
# also week day (as integer or factor in system locale)
today() %>% wday()
```

    ## [1] 6

``` r
today() %>% wday(label = TRUE)
```

    ## [1] ven
    ## Levels: dom < lun < mar < mer < gio < ven < sab

``` r
today() %>% leap_year() # is it a leap year?
```

    ## [1] FALSE

``` r
today() %>% dst() # is it Daylight Savings Time?
```

    ## [1] FALSE

### Date arithmetic

Date arithmetic is hard! Lots of conventions and unspoken assumptions. What does "a month from now" mean exactly?

``` r
today() + days(1) # one day from now
```

    ## [1] "2018-05-19"

``` r
today() + months(1) # one month from now
```

    ## [1] "2018-06-18"

``` r
# Round dates:
today() %>% floor_date(unit = "month") # round down to first day of month
```

    ## [1] "2018-05-01"

``` r
today() %>% ceiling_date(unit = "month") # round up to first day of next month
```

    ## [1] "2018-06-01"

``` r
today() %>% ceiling_date(unit = "month") - days(1) # round up to last day of this month
```

    ## [1] "2018-05-31"

``` r
today() %>% rollback() # round down to last day of previous month
```

    ## [1] "2018-04-30"

``` r
today() %>% rollback(roll_to_first = T) # round down first day of same month
```

    ## [1] "2018-05-01"

### Construct dates from separate columns:

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
flights %>%
  select(year, month, day) %>%
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
flights %>%
  select(year, month, day) %>%
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

What's in a date? Obviously *day*, *month*, *year*. But also time zone! (by default UTC)

``` r
dmy("16/05-2018", tz = "Europe/Rome") == dmy("16/05-2018", tz = "Europe/London")
```

    ## [1] FALSE

### Higher- and lower- resolution dates and time

`dmy_hms` (and obvious permutations) parse date and times to seconds:

``` r
# Using different representations:
dmy_hms("17/05/2018T8:22,30")
```

    ## [1] "2018-05-17 08:22:30 UTC"

``` r
dmy_hms("17/05/2018T8:22.30")
```

    ## [1] "2018-05-17 08:22:30 UTC"

``` r
dmy_hms("17-05-2018 8:22:30")
```

    ## [1] "2018-05-17 08:22:30 UTC"

``` r
dmy_hms("17-05-2018 8-22-3")
```

    ## [1] "2018-05-17 08:22:03 UTC"

``` r
dmy_hms("17-05-2018 8-22-3")
```

    ## [1] "2018-05-17 08:22:03 UTC"

`hms` parses time-of-day values:

``` r
# Using different representations:
hms("12:30:00")
```

    ## [1] "12H 30M 0S"

``` r
hms("12.31.00")
```

    ## [1] "12H 31M 0S"

Both have variants for lower-resolution input:

``` r
# parse date and time to resolution of minutes
dmy_hm("17-05-2018 8-22")
```

    ## [1] "2018-05-17 08:22:00 UTC"

``` r
# parse date and time to precision of hours
dmy_h("17-05-2018 08")
```

    ## [1] "2018-05-17 08:00:00 UTC"

``` r
# time at diffrent resolution
hm("12.31") # with different separators
```

    ## [1] "12H 31M 0S"

``` r
ms("2.05") # with different separators
```

    ## [1] "2M 5S"
