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
library(sf)
```

    ## Linking to GEOS 3.13.0, GDAL 3.8.5, PROJ 9.5.1; sf_use_s2() is TRUE

get tract geometry dataset

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
tract_geo = tract_geo|>
  select(-variable, -estimate, -moe)
```

get 2020 Neighborhood Tabulation Areas (NTA) data

``` r
nta = st_read("data_import/2020_Neighborhood_Tabulation_Areas_(NTAs)_20261126.geojson")
```

    ## Reading layer `2020_Neighborhood_Tabulation_Areas_(NTAs)_20261126' from data source `/Users/lxy/Desktop/p8105_R/p8105_final_project_1/data_import/2020_Neighborhood_Tabulation_Areas_(NTAs)_20261126.geojson' 
    ##   using driver `GeoJSON'
    ## Simple feature collection with 262 features and 15 fields
    ## Geometry type: MULTIPOLYGON
    ## Dimension:     XY
    ## Bounding box:  xmin: -74.25559 ymin: 40.49613 xmax: -73.70001 ymax: 40.91553
    ## Geodetic CRS:  WGS 84

combine two dataset

``` r
## transform both dataset to the same projected CRS (EPSG:2263)
nta = st_transform(nta, 2263)
tract_geo = st_transform(tract_geo, 2263)

## calculate the spatial intersection between census tract and NTA
tract_nta = st_intersection(
  tract_geo |> select(GEOID, NAME),
  nta |> select(nta2020, ntaname, boroname)
)
```

    ## Warning: attribute variables are assumed to be spatially constant throughout
    ## all geometries

``` r
## calculate the overlapping area
tract_nta = tract_nta|>
  mutate(overlap_area = as.numeric(st_area(geometry)))

## assign each census tract to its primary NTA, select the NTA with the largest overlapping area for each Census Tract
tract_nta_main = tract_nta|>
  st_drop_geometry()|>
  group_by(GEOID)|>
  slice_max(overlap_area, n = 1, with_ties = F)|>
  ungroup()|>
  select(GEOID, nta2020, ntaname, boroname)

## join back to census tract dataset
tract_geo = tract_geo|>
  left_join(tract_nta_main, by = "GEOID")

## Identify census tracts without an NTA match
tract_geo = tract_geo|>
  mutate(
    nta_status = if_else(
      is.na(ntaname),
      "No NTA match",
      "Matched"
    )
  )
```

``` r
saveRDS(tract_geo, "descriptive_gym_analysis/tract_geo.rds")
```
