Project Proposal: Beyond the Gym
================

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

New York City is home to a diverse range of cultures and communities,
yet significant disparities exist in socioeconomic status and access to
healthcare. As the fitness industry evolves, gyms are becoming more than
just places for physical exercise; they increasingly reflect broader
patterns of lifestyle, consumer behavior, and access to health-related
resources. By examining the distribution, accessibility, and
characteristics of gyms across NYC, we aim to use them as a diagnostic
tool to explore deeper systemic issues in NYC. \### Motivation

New York City is home to a diverse range of cultures and communities,
with substantial differences in socioeconomic conditions, demographic
characteristics, and health outcomes. While access to healthcare is an
important aspect of public health, access to opportunities for physical
activity is another dimension worth examining. Fitness facilities,
including commercial gyms and public recreational centers, provide
important resources for physical activity. However, their distribution,
affordability, operating hours, and available amenities may vary across
neighborhoods, potentially creating differences in residents’ access to
fitness resources.

As the fitness industry evolves, gyms have become more than just places
for physical exercise. They also reflect differences in lifestyle,
consumer choices, and the availability of health-related resources
across communities. Understanding the fitness landscape therefore
requires looking beyond the number and location of facilities. Community
characteristics, such as income, population size, and age distribution,
may help explain patterns in facility distribution, while factors such
as membership fees, commuting distance, operating hours, and available
amenities determine whether these resources are accessible and suitable
for different groups.

With this in mind, our project examines the distribution,
characteristics, and accessibility of fitness resources across New York
City from several perspectives. We first develop a descriptive overview
of fitness facilities and their surrounding communities, exploring how
facility availability relates to neighborhood demographic and
socioeconomic characteristics. Building on this overview, we investigate
three specific questions: which fitness options best meet the needs and
practical constraints of Columbia students and faculty; whether
neighborhoods with greater fall-related health burdens among older
adults have sufficient resources for strength and balance training; and
how access to commercial gyms and public recreation centers varies
across communities with different levels of diabetes prevalence.

Together, these analyses aim to provide a broader understanding of NYC’s
fitness resource landscape, examining not only where facilities are
located, but also how their availability and characteristics relate to
the needs and circumstances of different populations and communities.
\## Intended final products

1.  An interactive NYC fitness resource map and descriptive dashboard
2.  A CUMC student fitness guide
3.  An NYC older adult fall-prevention resource report
4.  An NYC diabetes burden and fitness resource accessibility report
5.  A reproducible project website

## The anticipated data sources

[NYC Open Data](https://www.nyc.gov/opendata)  
[NYC gov](https://www.nyc.gov/main)  
[tidycensus R package](https://walker-data.com/tidycensus/)  
[OpenStreetMap](https://wiki.openstreetmap.org/wiki/Gym_/_Fitness_centre)  
[Overpass Turbo](https://overpass-turbo.eu/)  
[NYC Planning](https://www.nyc.gov/content/planning/pages/)  
[CDC Tract
Data](https://data.cdc.gov/500-Cities-Places/PLACES-Census-Tract-Data-GIS-Friendly-Format-2025-/yjkw-uj5s/about_data)  
[NYC Parks Directory of Recreation
Centers](https://data.cityofnewyork.us/Housing-Development/Directory-of-Recreation-Centers/ydj7-rk56)  
[U.S. Census Bureau TIGER/Line
Shapefiles](https://www.census.gov/cgi-bin/geo/shapefiles/index.php)  
[United States Census
Bureau](https://data.census.gov/table?q=B18105&g=9700000US4822380&y=2024)  
[GymEquipMap](https://gymequipmap.com)

## Related works

Kaufman, T. K. Neighborhood recreation facilities and facility
membership are jointly associated with objectively measured physical
activity. *Journal of Urban Health*,**2019**, *96*(4), 570–582.

Powell, L. M. Availability of physical activity-related facilities and
neighborhood demographic and socioeconomic characteristics: A national
study. *American Journal of Public Health*, **2006**, *96*(9),
1676–1680.

Cereijo, L. Access to and availability of exercise facilities in Madrid:
An equity perspective. *International Journal of Health Geographics*,
**2019**, *18*(15).

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
dataset, we will break the dataset down into three perspectives.

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

A third analysis will examine **fitness resource accessibility and
diabetes burden in NYC**. Using CDC PLACES census tract estimates, we
will map adult diabetes prevalence, compare nearby commercial gym counts
and distance to the nearest gym across communities with different
diabetes burdens, and assess how public recreation centers expand
coverage and where gaps remain. Visualizations will include facility
locations overlaid on diabetes prevalence maps, accessibility comparison
plots, and interactive maps contrasting commercial-only coverage with
combined commercial and public facility coverage. Findings will describe
community-level associations rather than causal effects.

## Coding challenges

- Data collection and integration from multiple sources

- Data cleaning, facility classification, and duplicate removal

- Geocoding and spatial joins

- Handling missing data and inconsistent geographic units

- Defining consistent distance thresholds and calculating facility
  accessibility

- Quantifying additional coverage from public recreation centers

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
