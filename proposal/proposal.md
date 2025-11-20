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
variables in the main structured table (prof_2018_2019). These variables
are `Category`, `WHE Bottom`, `WHE Top`, `# Children`, `Average`,
`# Below`, `% Below`, `# Meeting / Exceeding`, \`% Meeting / Exceeding
and Time Period.

For analysis. We did not analyze WHE Bottom, WHE Top, or Average, as we
used them only as benchmarks.

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
expectations. We will analyze the data based on 3 timelines (Spring,
Winter, and Fall) within a school year.

#### Graphs:

1.  Ridgeline Density Plot - General: We aim to show how the pandemic
    affected students overall. To visualize this, we plan to use a
    density ridgeline graph, where the x-axis represents the Season +
    Year and the y-axis represents the percentage of children meeting or
    exceeding expectations. We also plan to separate the data by
    category using facets for clearer comparisons.

2.  Facet Line Graph - Age Groups: We will specifically focus on how the
    COVID-19 pandemic impacted different age groups, ranging from 0
    to 5. We plan to use a line graph, where the x-axis represents the
    Season + Year and the y-axis represents the percentage of students
    who meet or exceed expectations. The graph will be faceted by
    category, and different line colors will represent each age group.

3.  Facet Density Plot - IEP Groups: We will use similar axes (x =
    Season + Year, y = percentage of students who meet or exceed
    expectations) and the same facet categories as in our second graph.
    However, instead of focusing on different age groups, this graph
    will compare students with IEPs to those without IEPs to determine
    whether children with IEPs were more affected by the pandemic. For
    now, this graph will include data only up to Winter 2023, since we
    do not yet have IEP data for the 2023–2024 and 2024–2025 academic
    years. We are currently waiting for that information from Monica.

#### Preliminary exploratory data analysis

##### Pre-Covid Graph

With this graph, we aim to understand how successful Promise Early
Education was during a pre-COVID academic year (2018-2019) by comparing
the percentage of students who met or exceeded expectations across the
fall, winter, and spring assessments. The x-axis represents the Fall,
Winter, and Spring assessments for the 2018–2019 academic year, while
the y-axis shows the percentage of students who met or exceeded
expectations. The graph includes six facets, each representing a
different learning domain: `Cognitive`, `Language`,
`Physical Development`, `Social-Emotional`, `Literacy`, and
`Mathematics`.

``` r
categorized_data_2018_2019 <- prof_2018_2019 |>
  group_by(`Time Period`, `Category`) |>
  summarise(
    `Total # Children` = sum(`# Children`, na.rm = TRUE), 
    `Meeting / Exceeding Children` = sum(`# Meeting / Exceeding`, na.rm = TRUE), 
    `% percentage` = round(`Meeting / Exceeding Children` / `Total # Children` * 100, 2),
    .groups = "drop"
  )
```

``` r
ggplot(categorized_data_2018_2019, aes(x = `Time Period`, y = `% percentage`)) +
  geom_col() +
  facet_wrap(~ `Category`) +
  ylim(0, 100) +
  labs(
    title = "Percentage of Children Meeting/Exceeding Expectations",
    subtitle = "by Time Period and Category",
    x = "Time Period",
    y = "Percentage (%)"
  ) + 
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

![](proposal_files/figure-gfm/mapping-categorized-table-1.png)<!-- -->

Thanks to this graph, we can see how successful Promise Early Education
was in categories like `Physical`. Moreover, we can see the growth of
the students from the beggining (Fall) to the end of the school year
(Winter and Sping), especially in categories like `Cognitive` and
`Social-Emotional` where the percentage grew from around 50% to over
80%.

##### Facet Line Graph

``` r
library(tidyverse)

# Check which datasets exist
datasets_needed <- c("X2018_2019", "X2020_2021", "X2021_2022", "X2022_2023", "X2023_2024", "X2024_2025")
existing_data <- datasets_needed[sapply(datasets_needed, exists)]
missing_data <- datasets_needed[!sapply(datasets_needed, exists)]

print("Datasets found:")
```

    ## [1] "Datasets found:"

``` r
print(existing_data)
```

    ## character(0)

``` r
print("Datasets missing:")
```

    ## [1] "Datasets missing:"

``` r
print(missing_data)
```

    ## [1] "X2018_2019" "X2020_2021" "X2021_2022" "X2022_2023" "X2023_2024"
    ## [6] "X2024_2025"

``` r
# If data is missing, show available objects
if(length(missing_data) > 0) {
  print("Available objects in environment:")
  print(ls())
}
```

    ## [1] "Available objects in environment:"
    ## [1] "categorized_data_2018_2019" "datasets_needed"           
    ## [3] "existing_data"              "missing_data"              
    ## [5] "prof_2018_2019"

``` r
library(tidyverse)
library(readxl)
```

``` r
# Check if datasets exist, if not show error message
required_data <- c("X2018_2019", "X2020_2021", "X2021_2022", "X2022_2023", "X2023_2024", "X2024_2025")

# Only run if all data exists
if(all(sapply(required_data, exists))) {
  
  # Clean function
  fix_data <- function(d){
    d |>
      select(Category, Age, `Time Period`, `# Children`, `# Meeting / Exceeding`) |>
      mutate(
        `# Children` = as.numeric(`# Children`),
        `# Meeting / Exceeding` = as.numeric(`# Meeting / Exceeding`)
      )
  }
  
  # Combine data
  data <- bind_rows(
    fix_data(X2018_2019), fix_data(X2020_2021), fix_data(X2021_2022),
    fix_data(X2022_2023), fix_data(X2023_2024), fix_data(X2024_2025)
  ) |>
    mutate(
      season = str_extract(`Time Period`, "Fall|Winter|Spring"),
      yr = as.integer(str_extract(`Time Period`, "20\\d{2}")),
      start = case_when(
        yr %in% c(2018, 2019) ~ 2018,
        yr %in% c(2024, 2025) ~ 2024,
        TRUE ~ yr
      ),
      label = paste(season, paste0(start, "-", start + 1)),
      order = start*10 + match(season, c("Fall","Winter","Spring"))
    ) |>
    filter(!is.na(season)) |>
    group_by(label, Category, Age, order) |>
    summarise(
      percentage = sum(`# Meeting / Exceeding`, na.rm = TRUE) / sum(`# Children`, na.rm = TRUE) * 100,
      .groups = "drop"
    )
  
  # Make plot
  ggplot(data, aes(reorder(label, order), percentage, color = Age, group = Age)) +
    geom_line(linewidth = 1, alpha = 0.6) +
    geom_point(size = 2, alpha = 0.75) +
    facet_wrap(~ Category, nrow = 2) +
    scale_color_viridis_d() +
    labs(title = "COVID-19 Impact on Age Groups", x = "Time Period", y = "Percentage (%)") +
    theme_minimal() +
    theme(axis.text.x = element_text(angle = 90, hjust = 1), strip.text = element_text(face = "bold"))
  
} else {
  print("ERROR: Missing datasets. You need to load your Excel files first!")
  print("Add a chunk like this BEFORE this graph:")
  print("X2018_2019 <- read_excel('path/to/your/file.xlsx')")
}
```

    ## [1] "ERROR: Missing datasets. You need to load your Excel files first!"
    ## [1] "Add a chunk like this BEFORE this graph:"
    ## [1] "X2018_2019 <- read_excel('path/to/your/file.xlsx')"
