Project proposal
================
Gold Analysts - Mekkawy, Nissan, Razvan

``` r
library(tidyverse)
library(broom)
library(readxl)
library(dplyr)
library(skimr)
```

## 1. Intro

We are developing our research based on a database provided by Promise
Early Education Programs: Early Head Start and Head Start. They focus on
children’s developmental outcomes.

The data is collected using the Teaching Strategies Gold (TS GOLD)
assessment, which analyzes growth towards Widely Held Expectations (WHE)
for typically developing children at each stage.

This collection method categorizes children’s performance in every vital
classification: Physical Examination, Language, Cognitive,
Social-Emotional, Literacy and Mathematics.

We plan on researching how COVID-19 impacted different groups of
students. We will analyze these groups in two categories: based on their
age or based on whether they have an Individualized Educational Program
(IEP) or not.

The dataset used for this analysis contains 180 observations and 10
variables in the main structured table (prof_2018_2019).These variables
are Category, WHE Bottom, WHE Top, \# Children, Average, \# Below, %
Below, \# Meeting / Exceeding, % Meeting / Exceeding, and Time Period.
In our analysis, we included Category, \# Children, \# Below, % Below,
\# Meeting / Exceeding, % Meeting / Exceeding, and Time Period, while
WHE Bottom, WHE Top, and Average were not included as analytic outcomes
and were used only as benchmarks/reference.

## 2. Data

We are currently tidying up the 6 datasets we plan on using for our
research. Each of them presents specific data collected in a school year
(e.g. 2018-2019, 2023-2024).

Meanwhile, since the datasets from the NGO have the same variables, we
will use a past dataset to explain the structure. Our variables are: -
`Bottom`: Lowest Score (for agency/ classroom) - `Top`: Highest Score
(for agency/ classroom - `# Children`: Total \# of children assessed -
`Average` : Average Score of children (for agency/ classroom) -
`# Below` :# of children below developmental expectations - `% Below` :
% of children below developmental expectations

``` r
prof_2018_2019 <- read_excel("../data/ignore/file_show.xlsx")
```

``` r
glimpse(prof_2018_2019)
```

    ## Rows: 180
    ## Columns: 10
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `WHE Bottom`            <dbl> 300, 300, 300, 300, 300, 300, 300, 300, 300, 3…
    ## $ `WHE Top`               <dbl> 396, 396, 396, 396, 396, 396, 396, 396, 396, 3…
    ## $ `# Children`            <dbl> 1, 7, 3, 11, 11, 8, 9, 9, 1, 11, 1, 7, 3, 11, …
    ## $ Average                 <dbl> 254, 302, 268, 347, 280, 299, 317, 373, 341, 2…
    ## $ `# Below`               <dbl> 1, 4, 3, 2, 8, 3, 1, 1, NA, 10, 1, 1, NA, NA, …
    ## $ `% Below`               <dbl> 100.0, 57.1, 100.0, 18.2, 72.7, 37.5, 11.1, 11…
    ## $ `# Meeting / Exceeding` <dbl> NA, 3, NA, 9, 3, 5, 8, 8, 1, 1, NA, 6, 3, 11, …
    ## $ `% Meeting / Exceeding` <dbl> 0.0, 42.9, 0.0, 81.8, 27.3, 62.5, 88.9, 88.9, …
    ## $ `Time Period`           <chr> "Fall 2018/2019", "Fall 2018/2019", "Fall 2018…

``` r
skim(prof_2018_2019)
```

|                                                  |                |
|:-------------------------------------------------|:---------------|
| Name                                             | prof_2018_2019 |
| Number of rows                                   | 180            |
| Number of columns                                | 10             |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |                |
| Column type frequency:                           |                |
| character                                        | 2              |
| numeric                                          | 8              |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |                |
| Group variables                                  | None           |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| Category      |         0 |             1 |   8 |  16 |     0 |        6 |          0 |
| Time Period   |         0 |             1 |  14 |  16 |     0 |        3 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate | mean | sd | p0 | p25 | p50 | p75 | p100 | hist |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|:---|
| WHE Bottom | 0 | 1.00 | 336.67 | 57.38 | 269.0 | 295.00 | 320.0 | 378.00 | 438 | ▇▁▂▂▂ |
| WHE Top | 0 | 1.00 | 476.67 | 77.18 | 390.0 | 396.00 | 461.5 | 555.00 | 596 | ▇▃▃▁▇ |
| \# Children | 0 | 1.00 | 7.08 | 3.80 | 1.0 | 3.00 | 8.5 | 11.00 | 11 | ▇▁▂▇▇ |
| Average | 0 | 1.00 | 395.13 | 102.52 | 213.0 | 314.75 | 380.0 | 453.00 | 738 | ▆▇▆▁▁ |
| \# Below | 72 | 0.60 | 3.14 | 2.70 | 1.0 | 1.00 | 2.0 | 4.00 | 11 | ▇▂▁▁▁ |
| % Below | 72 | 0.60 | 43.91 | 30.97 | 9.1 | 18.20 | 36.4 | 67.88 | 100 | ▇▅▁▃▃ |
| \# Meeting / Exceeding | 13 | 0.93 | 5.60 | 3.46 | 0.0 | 2.00 | 6.0 | 9.00 | 11 | ▇▅▂▅▇ |
| % Meeting / Exceeding | 0 | 1.00 | 73.66 | 32.23 | 0.0 | 57.10 | 88.9 | 100.00 | 100 | ▁▂▁▂▇ |

## 3. Data analysis plan

We will analyze our data from the following perspective: - Pre-COVID-19:
`2018_2019` - COVID-19: `2020_2021` and `2021_2022` - Post-COVID-19:
`2022_2023` , `2023_2024` and `2024_2025`

For our research questions, we will analyze the overall performance in
each general academic category: `Cognitive`, `Language`, `Literacy`,
`Mathematics`, `Physical`, and `Social-Emotional`.

For an in-depth categorization of our data, we will divide the data
based on `IEP` and `Age`.

To compare student success between these groups, we decided to create a
new variable representing the percentage of students who meet or exceed
expectations. Since the data is divided into semesters, we will combine
the answers into one year. We will create a new variable that will store
that number.

#### Graphs:

1.  Ridgeline Density Plot - General: We aim to show how the pandemic
    affected students overall. To visualize this, we plan to use a
    density ridgeline graph, where the x-axis represents the school year
    and the y-axis represents the percentage of children meeting or
    exceeding expectations. We also plan to separate the data by
    category using facets for clearer comparisons.

2.  Facet Line Graph - Age Groups: We will specifically focus on how the
    COVID-19 pandemic impacted different age groups, ranging from 0
    to 5. We plan to use a line graph, where the x-axis represents the
    school year and the y-axis represents the percentage of students who
    meet or exceed expectations. The graph will be faceted by category,
    and different line colors will represent each age group.

3.  Facet Density Plot - IEP Groups: We will use similar axes (x =
    school year, y = percentage of students who meet or exceed
    expectations) and the same facet categories as in our second graph.
    However, instead of focusing on different age groups, this graph
    will compare students with IEPs to those without IEPs to determine
    whether children with IEPs were more affected by the pandemic. For
    now, this graph will include data only up to Winter 2023, since we
    do not yet have IEP data for the 2023–2024 and 2024–2025 academic
    years. We are currently waiting for that information from Monica.
