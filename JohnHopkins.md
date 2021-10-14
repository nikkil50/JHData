JohnHopkins
================
N.L
10/14/2021

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
```
