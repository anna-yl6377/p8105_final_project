tract_geometry
================
Xieyu Liu
2026-11-25

``` r
library(tidycensus)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
v24 = load_variables(2024, "acs5")
```

``` r
tract_geo = get_acs(
  geography = "tract",
  variables = "B01003_001",
  state = "NY",
  county = c(
    "Bronx",
    "Kings",
    "New York",
    "Queens",
    "Richmond"
  ),
  year = 2024,
  geometry = T
)
```

    ## Getting data from the 2020-2024 5-year ACS

    ## Downloading feature geometry from the Census website.  To cache shapefiles for use in future sessions, set `options(tigris_use_cache = TRUE)`.

``` r
saveRDS(tract_geo, "descriptive_gym_analysis/tract_geo.rds")
```
