Project Proposal: Beyond the Gym
================
2026-11-09

## Group Members

Hongtong Lin (hl3464)  
Shiyu Kang (sk5855)  
Xieyu Liu (xl3712)  
Luyao Mao (lm4199)  
Yixuan Li (yl6377)

## Tentative project title

<span style="background-color: yellow;">Beyond the Gym: Exploring
Socioeconomic Inequality and Health Equity in New York City</span>

## Motivation for this project

New York City is home to a lot of different cultures and communities,
but there are huge gaps in socioeconomic status and health care
resources. Right now, gyms in NYC are transforming fast and no longer
serve simply as fitness places. We want to use these gyms as a
diagnostic tool to discuss deeper, systemic issues in NYC.

## Intended final products

1.  An interactive NYC fitness resource map and descriptive dashboard
2.  A CUMC student fitness guide
3.  An NYC older adult fall-prevention resource report
4.  An NYC diabetes and fitness resource accessibility report
5.  A reproducible project website

## The anticipated data sources

[NYC Open Data](https://www.nyc.gov/opendata)  
[NYC gov](https://www.nyc.gov/main)  
[tidycensus R package](https://walker-data.com/tidycensus/)  
[OpenStreetMap](https://wiki.openstreetmap.org/wiki/Gym_/_Fitness_centre) 
[Overpass Turbo](https://overpass-turbo.eu/) [NYC
Planning](https://www.nyc.gov/content/planning/pages/)  
[CDC Tract
Data](https://data.cdc.gov/500-Cities-Places/PLACES-Census-Tract-Data-GIS-Friendly-Format-2025-/yjkw-uj5s/about_data)  
[United States Census
Bureau](https://data.census.gov/table?q=B18105&g=9700000US4822380&y=2024)

## The planned analyses / visualizations

1.  Descriptive spatial analysis: geographic distribution and density of
    different fitness facilities across NYC.

2.  Ecological analysis: Associations between neighborhood-level fitness
    resource availability and demographic/socioeconomic characteristics,
    including population density, age distribution, income, education,
    and insurance coverage.

3.  Relative resource availability analysis: Number of fitness
    facilities per 10,000 residents across coverage.

4.  Geospatial accessibility analysis: Geographic proximity and
    distribution of commercial and public fitness resources across
    neighborhoods.

After showing the descriptive statistics and broad analyses from the
dataset, we will break the dataset dwon into three perspectives.

One analysis will be the best gym for a CUMC student in NYC.We would
compare commercial gyms with CUIMC Athletic Center and Dodge Fitness
Center for CUIMC students and faculty, considering membership fees,
commuting time and cost from campus housing, opening hours, and
equipment for different needs, such as strength and cardio training.

Another analysis will focus on the **fall prevention gap for older
adults in NYC**. The core question will ask if the
neighborhoods/boroughs with the highest fall hospitalization rates among
65+ adults have the fewest places to do strength and balance training.
Potential visualizations would be side-by-side maps of the community
districts/boroughs that display the number of fall-related
hospitalization on one side and the number of exercise places on the
other side. We might also show an interactive quadrant plot to see which
places have fewer exercise facilities but higher fall-related
hospitalizations rates. If time allows, we will also use the `survey` R
package to predict older adults’ behavior: Are 65+ respondents who live
near more gyms/public athletic facilities exercise more after adjusting
for factors like insurance and income.

## Coding challenges

- Data collection and integration from multiple sources

- Data cleaning, facility classification, and duplicate removal

- Geocoding and spatial joins

- Handling missing data and inconsistent geographic units

## The planned timeline

- Weekly meetings at **2:30 PM on Tuesdays**. Will meet virtually or
  cancel the meeting if not enough issues need to be addressed.
- November 13 by 12pm: Proposal submission
- November 09 - November 17: Exploring and cleaning data
- November 17 (Tuesday): Start to analyze data
- November 24 (Tuesday): Start to draft the Review Report
- December 1 (Tuesday): Review Report first draft review
- December 8 (Tuesday): Review Report second draft review: submit if no
  issues remain
- December 9 (Wednesday): Start to do web/screen-cast video
- December 9-11: Merge the videos together
- December 11 (Friday): Submit the web/screen-cast
- December 12 (Saturday): Peer assessment submission
