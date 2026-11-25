acs_data
================
Xieyu Liu
2026-11-23

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

# Population by age and sex

Get population by age and sex data

``` r
age_data <- get_acs(
  geography = "tract",
  table = "B01001",
  state = "NY",
  county = c(
    "Bronx",
    "Kings",
    "New York",
    "Queens",
    "Richmond"
  ),
  year = 2024,
  survey = "acs5"
)
```

    ## Getting data from the 2020-2024 5-year ACS

Clean name: 1.population by age and sex 2.separate tract, borough, and
state(removed)

``` r
age_data = age_data|>
  left_join(
    v24|>
      filter(str_detect(name, "^B01001_"))|>
      select(name, label),
    by = c("variable" = "name")
  )|>
  mutate(
    clean_name = label|>
      str_remove("Estimate!!")|>
      str_remove(":$")|>
      str_replace_all("!!","_")|>
      str_to_lower()|>
      str_replace_all("[^a-z0-9]+","_")
  )

age_data = age_data |>
  select(-variable, -label)

age_data = age_data|>
  separate(
    NAME,
    into = c("tract", "borough","state"),
    sep = ";",
    remove = T
  )

age_data = age_data|>
  mutate(
    tract = str_remove(tract, "Census Tract"),
    borough = str_remove(borough, "County")
  )|>
  select(-state)
```

Aggregate age groups into 4 categories: under 18, 18-34, 35-64, 65 and
over

``` r
age_data = age_data|>
  mutate(
    category = case_when(
      clean_name == "total" ~ "total",
      clean_name == "total_male" ~ "total_male",
      clean_name == "total_female" ~ "total_female",
      grepl("^total_male_(under_5|5_to_9|10_to_14|15_to_17)", clean_name) ~ "total_male_under_18",
      grepl("total_male_(18_and_19|20_years|21_years|22_to_24|25_to_29|30_to_34)", clean_name) ~ "total_male_18_to_34_years",
      grepl("total_male_(35_to_39|40_to_44|45_to_49|50_to_54|55_to_59|60_and_61|62_to_64)", clean_name) ~ "total_male_35_to_64_years",
      grepl("total_male_(65_and_66|67_to_69|70_to_74|75_to_79|80_to_84|85_years)", clean_name) ~ "total_male_65_and_over",
      
      grepl("^total_female_(under_5|5_to_9|10_to_14|15_to_17)", clean_name) ~ "total_female_under_18",
      grepl("total_female_(18_and_19|20_years|21_years|22_to_24|25_to_29|30_to_34)", clean_name) ~ "total_female_18_to_34_years",
      grepl("total_female_(35_to_39|40_to_44|45_to_49|50_to_54|55_to_59|60_and_61|62_to_64)", clean_name) ~ "total_female_35_to_64_years",
      grepl("total_female_(65_and_66|67_to_69|70_to_74|75_to_79|80_to_84|85_years)", clean_name) ~ "total_female_65_and_over",
      
      TRUE ~ NA_character_
    )
  )
```

Aggregate estimates and margins of error(MOEs)

``` r
# Four age groups, separated by sex
population_by_age_and_sex = age_data |>
  group_by(GEOID, tract, borough, category)|>
  summarise(
    estimate = sum(estimate),
    moe = moe_sum(moe, estimate),
    .groups = "drop"
  )

# Four age groups, combined sexes
population_by_age = age_data|>
  filter(grepl("^total$|^total_(male|female)_", category))|>
  mutate(
    category = sub("^total_(male|female)_","total_",category)
  )|>
  group_by(GEOID, tract, borough, category) |>
  summarise(
    estimate = sum(estimate),
    moe = moe_sum(moe, estimate),
    .groups = "drop"
  )
```

``` r
saveRDS(population_by_age_and_sex, "descriptive_gym_analysis/population_by_age_and_sex.rds")
saveRDS(population_by_age, "descriptive_gym_analysis/population_by_age.rds")
```
