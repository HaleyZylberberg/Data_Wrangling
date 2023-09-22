Data Wrangling L1
================

Let’s import the FAS_litters.csv using a relative path.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
liters_df=
  read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
liters_df = 
  janitor::clean_names(liters_df)
```

Let’s import the FAS_litters.csv using an absolute path. Having issues
with this, maybe bec of spaces in file names.

``` r
liters_df_abs=
  read_csv("~Desktop/Fall2023/DataScience/Lectures/DataWrangling/Data/FAS_litters.csv")

liters_df_abs = 
  janitor::clean_names(liters_df_abs)

head(liters_df)

tail(liters_df)
```

``` r
View(liters_df)
```

Look at data summary

``` r
str(liters_df)
```

    ## spc_tbl_ [49 × 8] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ group          : chr [1:49] "Con7" "Con7" "Con7" "Con7" ...
    ##  $ litter_number  : chr [1:49] "#85" "#1/2/95/2" "#5/5/3/83/3-3" "#5/4/2/95/2" ...
    ##  $ gd0_weight     : num [1:49] 19.7 27 26 28.5 NA NA NA NA NA 28.5 ...
    ##  $ gd18_weight    : num [1:49] 34.7 42 41.4 44.1 NA NA NA NA NA NA ...
    ##  $ gd_of_birth    : num [1:49] 20 19 19 19 20 20 20 20 20 20 ...
    ##  $ pups_born_alive: num [1:49] 3 8 6 5 6 6 9 9 8 8 ...
    ##  $ pups_dead_birth: num [1:49] 4 0 0 1 0 0 0 1 0 0 ...
    ##  $ pups_survive   : num [1:49] 3 7 5 4 6 4 9 8 8 8 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Group = col_character(),
    ##   ..   `Litter Number` = col_character(),
    ##   ..   `GD0 weight` = col_double(),
    ##   ..   `GD18 weight` = col_double(),
    ##   ..   `GD of Birth` = col_double(),
    ##   ..   `Pups born alive` = col_double(),
    ##   ..   `Pups dead @ birth` = col_double(),
    ##   ..   `Pups survive` = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
skimr::skim(liters_df)
```

|                                                  |           |
|:-------------------------------------------------|:----------|
| Name                                             | liters_df |
| Number of rows                                   | 49        |
| Number of columns                                | 8         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |           |
| Column type frequency:                           |           |
| character                                        | 2         |
| numeric                                          | 6         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Group variables                                  | None      |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |             1 |   4 |   4 |     0 |        6 |          0 |
| litter_number |         0 |             1 |   3 |  15 |     0 |       49 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |   p0 |   p25 |   p50 |   p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|-----:|------:|------:|------:|-----:|:------|
| gd0_weight      |        15 |          0.69 | 24.38 | 3.28 | 17.0 | 22.30 | 24.10 | 26.67 | 33.4 | ▃▇▇▆▁ |
| gd18_weight     |        17 |          0.65 | 41.52 | 4.05 | 33.4 | 38.88 | 42.25 | 43.80 | 52.7 | ▃▃▇▂▁ |
| gd_of_birth     |         0 |          1.00 | 19.65 | 0.48 | 19.0 | 19.00 | 20.00 | 20.00 | 20.0 | ▅▁▁▁▇ |
| pups_born_alive |         0 |          1.00 |  7.35 | 1.76 |  3.0 |  6.00 |  8.00 |  8.00 | 11.0 | ▁▃▂▇▁ |
| pups_dead_birth |         0 |          1.00 |  0.33 | 0.75 |  0.0 |  0.00 |  0.00 |  0.00 |  4.0 | ▇▂▁▁▁ |
| pups_survive    |         0 |          1.00 |  6.41 | 2.05 |  1.0 |  5.00 |  7.00 |  8.00 |  9.0 | ▁▃▂▇▇ |

Import pups dataset

``` r
pups_df=
  read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = 
  janitor::clean_names(pups_df)
```

\#Options in ’read\_\*’

Col_names - assignes first row as names. And Skip skips rows.

``` r
liters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
  read_csv("data/FAS_litters.csv",
  skip = 10, col_names = FALSE)
```

    ## Rows: 40 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): X1, X2
    ## dbl (6): X3, X4, X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## # A tibble: 40 × 8
    ##    X1    X2                 X3    X4    X5    X6    X7    X8
    ##    <chr> <chr>           <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1 Con8  #3/5/2/2/95      28.5  NA      20     8     0     8
    ##  2 Con8  #5/4/3/83/3      28    NA      19     9     0     8
    ##  3 Con8  #1/6/2/2/95-2    NA    NA      20     7     0     6
    ##  4 Con8  #3/5/3/83/3-3-2  NA    NA      20     8     0     8
    ##  5 Con8  #2/2/95/2        NA    NA      19     5     0     4
    ##  6 Con8  #3/6/2/2/95-3    NA    NA      20     7     0     7
    ##  7 Mod7  #59              17    33.4    19     8     0     5
    ##  8 Mod7  #103             21.4  42.1    19     9     1     9
    ##  9 Mod7  #1/82/3-2        NA    NA      19     6     0     6
    ## 10 Mod7  #3/83/3-2        NA    NA      19     8     0     8
    ## # ℹ 30 more rows

Look at NA values. Here we say treat NA and 19 as missing.

``` r
liters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
  read_csv("data/FAS_litters.csv",
  na= c("NA", 19 ))
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## # A tibble: 49 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>                  <dbl>         <dbl>         <dbl>
    ##  1 Con7  #85                     19.7          34.7            20
    ##  2 Con7  #1/2/95/2               27            42              NA
    ##  3 Con7  #5/5/3/83/3-3           26            41.4            NA
    ##  4 Con7  #5/4/2/95/2             28.5          44.1            NA
    ##  5 Con7  #4/2/95/3-3             NA            NA              20
    ##  6 Con7  #2/2/95/3-2             NA            NA              20
    ##  7 Con7  #1/5/3/83/3-3/2         NA            NA              20
    ##  8 Con8  #3/83/3-3               NA            NA              20
    ##  9 Con8  #2/95/3                 NA            NA              20
    ## 10 Con8  #3/5/2/2/95             28.5          NA              20
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

Column types Change variables from numeric to character to factor etc.

``` r
liters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
  read_csv("data/FAS_litters.csv",
  col_types = 
    cols(
      Group = col_factor()
    ))
```

    ## # A tibble: 49 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <fct> <chr>                  <dbl>         <dbl>         <dbl>
    ##  1 Con7  #85                     19.7          34.7            20
    ##  2 Con7  #1/2/95/2               27            42              19
    ##  3 Con7  #5/5/3/83/3-3           26            41.4            19
    ##  4 Con7  #5/4/2/95/2             28.5          44.1            19
    ##  5 Con7  #4/2/95/3-3             NA            NA              20
    ##  6 Con7  #2/2/95/3-2             NA            NA              20
    ##  7 Con7  #1/5/3/83/3-3/2         NA            NA              20
    ##  8 Con8  #3/83/3-3               NA            NA              20
    ##  9 Con8  #2/95/3                 NA            NA              20
    ## 10 Con8  #3/5/2/2/95             28.5          NA              20
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

\#Other file types

Import an xlx file first. First load in readdxl library

``` r
  library(readxl)
```

``` r
  mlb_df=
    read_excel("data/mlb11.xlsx")
```

Import a sas file.

``` r
  library(haven)
```

``` r
  pulse_df=
    read_sas("data/public_pulse_data.sas7bdat")
```

``` r
View(pulse_df)
```

\#Base R

``` r
liters_df = 
  read.csv("data/FAS_litters.csv")

liters_df$Gr
```

Dont use \$ because it calls in all variables with the same beginning if
you dont type it out full name.

\#Export Data

We want to export data.

``` r
liters_df_cleaned=
  read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
liters_df_cleaned = 
  janitor:: clean_names(liters_df_cleaned)

write_csv(liters_df_cleaned, "data/liters_cleaned.csv")
```
