nyc_gym_main
================
Xieyu Liu
2026-11-19

``` r
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
library(jsonlite)
```

    ## 
    ## Attaching package: 'jsonlite'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     flatten

Data cleaning: OSM fitness facilities

``` r
data = fromJSON("data_import/nyc_fitness_facilities_main.json") # Extract the elements from the orginal JSON data

gym_data = data[["elements"]]|>
  unnest_wider(tags, names_sep = "_")|>
  unnest_wider(center, names_sep = "_")|> # expand the nested tags and center columns into separate columns
  select(type,
         id,
         lat,
         lon,
         center_lat,
         center_lon,
         `tags_addr:city`,
         `tags_addr:postcode`,
         tags_name,
         tags_opening_hours,
         tags_leisure,
         tags_sport
         )|> # select relavant variables
  rename_with(~ str_remove(.x, "^tags_"))|>
  rename_with(~ str_remove(.x, "^addr:")) # Rename columns to remove the "tags_" and "addr:" prefixes
```

``` r
gym_data = gym_data|>
  mutate(
    lat = coalesce(lat, center_lat),
    lon = coalesce(lon, center_lon)
  ) 
# Nodes have their own latitude and longitude
# For ways and relations, use the center coordinates (center_lat and center_lon) to represent their locations
```
