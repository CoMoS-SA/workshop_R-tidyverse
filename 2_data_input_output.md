Data input and output
================
Matteo Sostero

**Packages needed for this session**:

-   `tidyverse`
-   `readxl` (installed with tidyverse)
-   `haven` (installed with tidyverse)
-   `naniar` (new)

Load the packages for this session
----------------------------------

`tidyverse` loads (eight) packages of the *tidyverse* and shows their version. Also load `readxl` to read Excel files and `haven` for importing and exporting Stata, SAS and SPSS data.

``` r
library(tidyverse)
```

    ## -- Attaching packages ----------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.4
    ## v tibble  1.4.2     v dplyr   0.7.4
    ## v tidyr   0.8.0     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts -------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(haven)
library(naniar) 
```

Data input and output
---------------------

Import a table with `read_csv` (NB, different than `read.csv`!). `read_csv` parses variables by guessing the column types based on heuristics:

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

Let's try with a tricky file

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

open the raw `csv` file to see what's happening (hint: line 1001):

we help `read_csv` parser by scanning more rows before guessing type:

``` r
challenge <- read_csv("./data/challenge.csv", guess_max = 1500)
```

    ## Parsed with column specification:
    ## cols(
    ##   x = col_double(),
    ##   y = col_date(format = "")
    ## )

we can also specify column types manually:

``` r
challenge <- read_csv("./data/challenge.csv", col_types = list(x = col_double(), y = col_date()))
```

\_pro-tip\_\_: import problematic columns as character and inspect them:

``` r
challenge <- read_csv("./data/challenge.csv", col_types = list(x = col_character(), y = col_character()))

challenge %>% pull(y) %>% sort() %>% unique()
```

    ##  [1] "2010-01-03" "2010-01-04" "2010-01-05" "2010-01-09" "2010-01-16"
    ##  [6] "2010-01-27" "2010-02-14" "2010-02-20" "2010-02-28" "2010-03-17"
    ## [11] "2010-03-19" "2010-03-23" "2010-03-24" "2010-03-26" "2010-03-27"
    ## [16] "2010-03-28" "2010-04-17" "2010-04-25" "2010-05-09" "2010-05-10"
    ##  [ reached getOption("max.print") -- omitted 890 entries ]

``` r
challenge %>% pull(x) %>% sort() %>% unique()
```

    ##  [1] "0.0024007875472307205" "0.0024924282915890217"
    ##  [3] "0.004081981023773551"  "0.006291386438533664" 
    ##  [5] "0.007070775609463453"  "0.008419594960287213" 
    ##  [7] "0.008509289706125855"  "0.00876278686337173"  
    ##  [9] "0.009083196753636003"  "0.01098793395794928"  
    ## [11] "0.014630335848778486"  "0.016221591737121344" 
    ## [13] "0.01808677427470684"   "0.018906170036643744" 
    ## [15] "0.019359473139047623"  "0.020153695717453957" 
    ## [17] "0.021540780318900943"  "0.02179576293565333"  
    ## [19] "0.02280205488204956"   "0.023566172923892736" 
    ##  [ reached getOption("max.print") -- omitted 1901 entries ]

`readr` tries to guess the type of object based on heuristics:

``` r
guess_parser("123")
```

    ## [1] "integer"

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

``` r
guess_parser("15/06/2018")
```

    ## [1] "character"

Read a file from a URL

``` r
flights_import <- read_csv("https://raw.githubusercontent.com/CoMoS-SA/workshop-R-tidyverse/master/data/flights.csv")
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

Importing Excel files with `readxl`
-----------------------------------

We can import Excel workbooks with `read_excel`: it works with `.xlsx` and `.xls` files.

``` r
# Enumerate sheets in the workbook
excel_sheets("./data/nycflights.xlsx")
```

    ## [1] "Flights"  "Airlines"

``` r
# Access a given sheet
flights_xl  <- read_excel("./data/nycflights.xlsx", sheet = "Flights")
airlines_xl <- read_excel("./data/nycflights.xlsx", sheet = "Airlines")
```

NB: the package `readxl` does not provide functions to *export* Excel workbooks, but the package `openxls` does.

Importing and exporting Stata `.dta` files using `haven`
--------------------------------------------------------

``` r
mtcars_stata <- read_dta("./data/mtcars.dta")
```

Saving data in R
----------------

The best format for saving R objects for later use is `.rds`

Dealing with missing values (`na`) using `naniar`
-------------------------------------------------
