JohnHopkins
================
N.L
10/14/2021

``` r
#Follow the steps of the Prof. to insert the data frame into RMD
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
url_in <- "http://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/"
file_names <-c("time_series_covid19_confirmed_global.csv",
               "time_series_covid19_deaths_global.csv",
               "time_series_covid19_confirmed_US.csv",
               "time_series_covid19_deaths_US.csv")
library(stringr)
urls <- str_c(url_in,file_names) 
library(tidyverse)
```

``` r
global_cases <- read_csv(urls[1])
```

    ## Rows: 279 Columns: 635

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (2): Province/State, Country/Region
    ## dbl (633): Lat, Long, 1/22/20, 1/23/20, 1/24/20, 1/25/20, 1/26/20, 1/27/20, ...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
global_deaths <- read_csv(urls[2])
```

    ## Rows: 279 Columns: 635

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (2): Province/State, Country/Region
    ## dbl (633): Lat, Long, 1/22/20, 1/23/20, 1/24/20, 1/25/20, 1/26/20, 1/27/20, ...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
US_cases <- read_csv(urls[3])
```

    ## Rows: 3342 Columns: 642

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (6): iso2, iso3, Admin2, Province_State, Country_Region, Combined_Key
    ## dbl (636): UID, code3, FIPS, Lat, Long_, 1/22/20, 1/23/20, 1/24/20, 1/25/20,...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
US_deaths<- read.csv(urls[4])

global_cases <-global_cases %>%
pivot_longer(cols = -c(`Province/State`,                  `Country/Region`, Lat,Long),
names_to = "date",
values_to = "cases") %>%
select(-c(Lat,Long))
global_cases
```

    ## # A tibble: 176,049 × 4
    ##    `Province/State` `Country/Region` date    cases
    ##    <chr>            <chr>            <chr>   <dbl>
    ##  1 <NA>             Afghanistan      1/22/20     0
    ##  2 <NA>             Afghanistan      1/23/20     0
    ##  3 <NA>             Afghanistan      1/24/20     0
    ##  4 <NA>             Afghanistan      1/25/20     0
    ##  5 <NA>             Afghanistan      1/26/20     0
    ##  6 <NA>             Afghanistan      1/27/20     0
    ##  7 <NA>             Afghanistan      1/28/20     0
    ##  8 <NA>             Afghanistan      1/29/20     0
    ##  9 <NA>             Afghanistan      1/30/20     0
    ## 10 <NA>             Afghanistan      1/31/20     0
    ## # … with 176,039 more rows

``` r
global_deaths <-global_deaths %>%
pivot_longer(cols = -c(`Province/State`,                  `Country/Region`, Lat,Long),
names_to = "date",
values_to = "deaths") %>%
select(-c(Lat,Long))
global_deaths
```

    ## # A tibble: 176,049 × 4
    ##    `Province/State` `Country/Region` date    deaths
    ##    <chr>            <chr>            <chr>    <dbl>
    ##  1 <NA>             Afghanistan      1/22/20      0
    ##  2 <NA>             Afghanistan      1/23/20      0
    ##  3 <NA>             Afghanistan      1/24/20      0
    ##  4 <NA>             Afghanistan      1/25/20      0
    ##  5 <NA>             Afghanistan      1/26/20      0
    ##  6 <NA>             Afghanistan      1/27/20      0
    ##  7 <NA>             Afghanistan      1/28/20      0
    ##  8 <NA>             Afghanistan      1/29/20      0
    ##  9 <NA>             Afghanistan      1/30/20      0
    ## 10 <NA>             Afghanistan      1/31/20      0
    ## # … with 176,039 more rows

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
global <-global_cases %>%
  full_join(global_deaths) %>%
  rename(Country_Region = `Country/Region`,
         Province_State = `Province/State`) %>%
  mutate(date = mdy(date))
```

    ## Joining, by = c("Province/State", "Country/Region", "date")

``` r
global
```

    ## # A tibble: 176,049 × 5
    ##    Province_State Country_Region date       cases deaths
    ##    <chr>          <chr>          <date>     <dbl>  <dbl>
    ##  1 <NA>           Afghanistan    2020-01-22     0      0
    ##  2 <NA>           Afghanistan    2020-01-23     0      0
    ##  3 <NA>           Afghanistan    2020-01-24     0      0
    ##  4 <NA>           Afghanistan    2020-01-25     0      0
    ##  5 <NA>           Afghanistan    2020-01-26     0      0
    ##  6 <NA>           Afghanistan    2020-01-27     0      0
    ##  7 <NA>           Afghanistan    2020-01-28     0      0
    ##  8 <NA>           Afghanistan    2020-01-29     0      0
    ##  9 <NA>           Afghanistan    2020-01-30     0      0
    ## 10 <NA>           Afghanistan    2020-01-31     0      0
    ## # … with 176,039 more rows

``` r
summary(global)
```

    ##  Province_State     Country_Region          date                cases         
    ##  Length:176049      Length:176049      Min.   :2020-01-22   Min.   :       0  
    ##  Class :character   Class :character   1st Qu.:2020-06-27   1st Qu.:     153  
    ##  Mode  :character   Mode  :character   Median :2020-12-02   Median :    2530  
    ##                                        Mean   :2020-12-02   Mean   :  307400  
    ##                                        3rd Qu.:2021-05-09   3rd Qu.:   57965  
    ##                                        Max.   :2021-10-13   Max.   :44684150  
    ##      deaths      
    ##  Min.   :     0  
    ##  1st Qu.:     1  
    ##  Median :    40  
    ##  Mean   :  7006  
    ##  3rd Qu.:   958  
    ##  Max.   :719558

``` r
global <- global %>% filter(cases > 0)

global %>% filter(cases > 44000000)
```

    ## # A tibble: 8 × 5
    ##   Province_State Country_Region date          cases deaths
    ##   <chr>          <chr>          <date>        <dbl>  <dbl>
    ## 1 <NA>           US             2021-10-06 44058827 708110
    ## 2 <NA>           US             2021-10-07 44158910 710502
    ## 3 <NA>           US             2021-10-08 44290052 712339
    ## 4 <NA>           US             2021-10-09 44317989 712618
    ## 5 <NA>           US             2021-10-10 44340183 712873
    ## 6 <NA>           US             2021-10-11 44456385 714055
    ## 7 <NA>           US             2021-10-12 44562693 716471
    ## 8 <NA>           US             2021-10-13 44684150 719558

``` r
US_cases <- US_cases %>%
   pivot_longer(cols = -(UID:Combined_Key),
                names_to = "date",
                values_to = "cases") %>%
   select(Admin2:cases) %>%
   mutate(date = mdy(date)) %>%
   select(-c(Lat,Long_))

US_deaths <- US_deaths %>%
   pivot_longer(cols = -(UID:Population),
                names_to = "date",
                values_to = "deaths") %>%
   select(Admin2:deaths) %>%
   mutate(date = mdy(date)) %>%
   select(-c(Lat,Long_))
```

    ## Warning: All formats failed to parse. No formats found.

``` r
global <- global %>%
   unite("Combined_Key",
         c(Province_State, Country_Region),
         sep = ",",
         na.rm = TRUE,
         remove = FALSE)


global
```

    ## # A tibble: 159,988 × 6
    ##    Combined_Key Province_State Country_Region date       cases deaths
    ##    <chr>        <chr>          <chr>          <date>     <dbl>  <dbl>
    ##  1 Afghanistan  <NA>           Afghanistan    2020-02-24     5      0
    ##  2 Afghanistan  <NA>           Afghanistan    2020-02-25     5      0
    ##  3 Afghanistan  <NA>           Afghanistan    2020-02-26     5      0
    ##  4 Afghanistan  <NA>           Afghanistan    2020-02-27     5      0
    ##  5 Afghanistan  <NA>           Afghanistan    2020-02-28     5      0
    ##  6 Afghanistan  <NA>           Afghanistan    2020-02-29     5      0
    ##  7 Afghanistan  <NA>           Afghanistan    2020-03-01     5      0
    ##  8 Afghanistan  <NA>           Afghanistan    2020-03-02     5      0
    ##  9 Afghanistan  <NA>           Afghanistan    2020-03-03     5      0
    ## 10 Afghanistan  <NA>           Afghanistan    2020-03-04     5      0
    ## # … with 159,978 more rows
