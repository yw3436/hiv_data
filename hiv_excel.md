HIV dataset excel version
================
Yuqi Wang

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(rvest)
```

    ## Loading required package: xml2

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     pluck

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(readxl)

knitr::opts_chunk$set(
  fig.width = 6,
  fig.asp = .6,
  out.width = "90%"
)

theme_set(theme_minimal() + theme(legend.position = "bottom"))

options(
  ggplot2.continuous.colour = "viridis",
  ggplot2.continuous.fill = "viridis"
)

scale_colour_discrete = scale_colour_viridis_d
scale_fill_discrete = scale_fill_viridis_d

set.seed(1)
```

First, upload all the excel datasets.

``` r
data11 = read_excel('./hiv_data/2011_1.xlsx', range = 'A8:AH48', col_names = FALSE) %>%
  janitor::clean_names() %>%
  select(x1, x5, x10, x12, x14, x16, x18, x19, x25, x29, x33, x34) %>%
  filter(!is.na(x5)) %>% 
  filter(!str_detect(x1, "poverty")) %>% 
  rename(
    category = x1,
    total_hiv_diag_N = x5,
    total_hiv_diag_per = x10,
    without_aids_N = x12,
    without_aids_per = x14,
    concurrent_aids_N = x16,
    concurrent_aids_per = x18,
    aids = x19,
    plwha = x25,
    death = x29,
    borough = x33,
    sex = x34
  ) %>%
  separate(aids, c("aids_N", "aids_per"), " ") %>% 
  separate(plwha, c("plwha_N", "plwha_per"), " ") %>% 
  separate(death, c("death_N", "death_per"), " ") %>% 
  hablar::retype() %>% select(-aids_per, -plwha_per, -death_per) %>% view()
```

    ## New names:
    ## * `` -> ...1
    ## * `` -> ...2
    ## * `` -> ...3
    ## * `` -> ...4
    ## * `` -> ...5
    ## * ...

    ## Warning: Expected 2 pieces. Additional pieces discarded in 32 rows [2, 3, 4, 5,
    ## 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 1 rows [1].

    ## Warning: Expected 2 pieces. Additional pieces discarded in 32 rows [2, 3, 4, 5,
    ## 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 1 rows [1].

    ## Warning: Expected 2 pieces. Additional pieces discarded in 32 rows [2, 3, 4, 5,
    ## 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 1 rows [1].

``` r
data11_d = read_excel('./hiv_data/2011_1.xlsx', range = 'A49:AH324', col_names = FALSE) %>%
  janitor::clean_names() %>%
  select(x1, x5, x10, x12, x14, x16, x18, x19, x25, x29, x33, x34) %>%
  filter(!is.na(x5)) %>% 
  filter(!str_detect(x1, "poverty")) %>% 
  rename(
    category = x1,
    total_hiv_diag_N = x5,
    total_hiv_diag_per = x10,
    without_aids_N = x12,
    without_aids_per = x14,
    concurrent_aids_N = x16,
    concurrent_aids_per = x18,
    aids = x19,
    plwha = x25,
    death = x29,
    borough = x33,
    sex = x34
  ) %>%
  separate(aids, c("aids_N", "aids_per"), " ") %>% 
  separate(plwha, c("plwha_N", "plwha_per"), " ") %>% 
  separate(death, c("death_N", "death_per"), " ") %>% 
  hablar::retype() %>% select(-aids_per, -plwha_per, -death_per) %>% view()
```

    ## New names:
    ## * `` -> ...1
    ## * `` -> ...2
    ## * `` -> ...3
    ## * `` -> ...4
    ## * `` -> ...5
    ## * ...
