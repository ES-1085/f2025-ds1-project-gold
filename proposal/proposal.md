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

# Handout Work

### Reading Data

``` r
X2018_2019 <- read_excel("../data/ignore/2018-2019.xlsx")
X2020_2021 <- read_excel("../data/ignore/2020-2021.xlsx")
X2021_2022 <- read_excel("../data/ignore/2021-2022.xlsx")
X2022_2023 <- read_excel("../data/ignore/2022-2023.xlsx")
X2023_2024 <- read_excel("../data/ignore/2023-2024.xlsx")
X2024_2025 <- read_excel("../data/ignore/2024-2025.xlsx")
```

### Cleaning the imported data and ordering it chronologically

``` r
general_data_table <- bind_rows(
  #for each year we need to first convert our number of children, number of meeting/exceeding, and percentage of meeting/exceeding in numerit values and create a year column that would help us with sorting and labeling
  X2018_2019 |>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`)), 
      year = "18-19"), 
  X2020_2021 |>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`)), 
      year = "20-21"), 
  X2021_2022|>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`)), 
      year = "21-22"), 
  X2022_2023|>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`)), 
      year = "22-23"), 
  X2023_2024|>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`), na = c("N/A", "NA", "#DIV/0!")), 
      year = "23-24"), 
  X2024_2025|>
    mutate(
      `# Children` = parse_number(as.character(`# Children`), na = c("N/A", "NA")), 
      `# Meeting / Exceeding` = parse_number(as.character(`# Meeting / Exceeding`), na = c("N/A", "NA")), 
      `% Meeting / Exceeding` = parse_number(as.character(`% Meeting / Exceeding`)), 
      year = "24-25")
  ) |>
  #shortening and simplifying the label for each school year and trimester
  mutate(
    season = case_when(
      str_detect(`Time Period`, "Fall") ~ "Fall",
      str_detect(`Time Period`, "Winter") ~ "Winter",
      str_detect(`Time Period`, "Spring") ~ "Spring"
    ),
    label = paste(season, year),
    #sorting for chronological order taking the beginning of the school year and the code for each season (Fall - 1, Winter - 2, Spring - 3)
    #e.g. Fall 2018-2019 -> 181, Winter 2021-2022 -> 212
    sort_num = as.numeric(str_sub(year, 1, 2)) * 10 + match(season, c("Fall","Winter","Spring")) 
  )
#ordering our data chronologically
general_data_table <- general_data_table |>
  mutate(
    label = fct_reorder(label, sort_num)
  )
```

### General Data Plot

\<\<\<\<\<\<\< HEAD

======= \#### First Attempt We found this plot too complicated for the
general analysis that we wanted to look at and also a bit similar to the
second, more detailed plot we had in plan.

``` r
general_data_plot <- ggplot(general_data_table, aes(x = label, y = `% Meeting / Exceeding`, color = Age, group = Age)) +
  geom_line(size = 1.1) +
  geom_point(size = 2) +
  facet_wrap(~ Category, ncol = 1) +
  ylim(0, 100)+
  labs(
    title = "%Meeting/Exceeding Over 6 School Years",
    subtitle = "by Category",
    x = "School Year (Season–Year)",
    y = "Percent Meeting/Exceeding"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5),
    strip.text = element_text(face = "bold"),
    panel.spacing = unit(1, "lines")
  )
```

    ## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `linewidth` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

``` r
general_data_plot
```

![](proposal_files/figure-gfm/general-plot-attempt-1-1.png)<!-- -->

``` r
#saving
ggsave("general_plot.png", general_data_plot, width = 10, height = 20, dpi = 300)
```

#### Second Attempt

``` r
#creating a new column that would help us highlight the beginning of the school year
average_general_data_table <- general_data_table |>
  mutate(is_fall = (`season` == "Fall"))

#calculating the average of all age groups' seasonal performance
average_general_data_table <- average_general_data_table |>
  group_by(Category, label, sort_num, is_fall) |>
  summarise(
    `Avg Meeting Exceeding` = mean(`% Meeting / Exceeding`, na.rm = TRUE),
    .groups = "drop"
  )

#plotting
average_general_data_plot <- ggplot(average_general_data_table, aes(x = label, y = `Avg Meeting Exceeding`, group = Category)) +
  geom_line(size = 1) +
  geom_point(aes(size = ifelse(is_fall, 4, NA)), shape = 20, stroke = 0) +
  geom_vline(xintercept = "Fall 20-21", linetype = "dotted", color = "#51C168")+
  geom_vline(xintercept = "Fall 21-22", linetype = "dotted", color = "#51C168")+
  annotate("rect", xmin="Fall 18-19", xmax="Fall 20-21", ymin = 40, ymax = 100, alpha = 0.1, fill = "#E7913E")+
  annotate("rect", xmin="Fall 18-19", xmax="Fall 21-22", ymin = 40, ymax = 100, alpha = 0.1, fill = "#5C57D8")+
  annotate("rect", xmin="Fall 21-22", xmax="Spring 24-25", ymin = 40, ymax = 100, alpha = 0.1, fill = "#FABA09")+
  geom_text( 
    aes(x = "Spring 18-19", y = 105, label = "Pre-COVID19"),
    size = 2) +
  geom_text( 
    aes(x = "Spring 20-21", y = 105, label = "During-COVID19"),
    size = 2) +
  geom_text( 
    aes(x = "Fall 23-24", y = 105, label = "Post-COVID19"),
    size = 2) +
  facet_wrap(~ Category, ncol = 2) +
  ylim(40, 110)+
  labs(
    title = "Average Performance",
    subtitle = "by Category, for all ages",
    x = "School Year (Season–Year)",
    y = "% Meeting / Exceeding"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    axis.text.x = element_text(angle = 90, hjust = 1, vjust = 0.5),
    legend.position = "none"
  )

average_general_data_plot
```

    ## Warning: Removed 72 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](proposal_files/figure-gfm/general-plot-attempt-2-1.png)<!-- -->

``` r
#saving
ggsave("average_general_plot.png", average_general_data_plot, width = 15, height = 10, dpi = 300)
```

    ## Warning: Removed 72 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

### Age Grouped Plot

``` r
# Fix all data files
data <- bind_rows(
  X2018_2019 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "18-19"),
  X2020_2021 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "20-21"), 
  X2021_2022 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "21-22"),
  X2022_2023 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "22-23"),
  X2023_2024 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "23-24"),
  X2024_2025 |> select(Category, `# Children`, Age, `# Meeting / Exceeding`, `Time Period`) |> 
    mutate(`# Children` = suppressWarnings(as.numeric(`# Children`)), 
           `# Meeting / Exceeding` = suppressWarnings(as.numeric(`# Meeting / Exceeding`)), 
           year = "24-25")
) |>
mutate(
season = case_when(
str_detect(`Time Period`, "Fall") ~ "F",
str_detect(`Time Period`, "Winter") ~ "W",
str_detect(`Time Period`, "Spring") ~ "S"
    ),
label = paste0(season, year),
sort_num = as.numeric(str_sub(year, 1, 2)) * 10 + match(season, c("F","W","S"))
  ) |>
drop_na() |>
group_by(label, Category, Age, sort_num, year, season) |>
summarise(percent = sum(`# Meeting / Exceeding`) / sum(`# Children`) * 100, .groups = "drop")

data <- data |>
filter(Age != "0-1") |>
drop_na()

data <- data |>
filter(Age != "1-2") |>
drop_na() 

# I will make the plot and save it to covid_plot variable
covid_plot <- ggplot(data, aes(reorder(label, sort_num), percent, color = Age, group = Age)) +
# Add red background highlight for COVID period (Fall 2019 to Spring 2020)
annotate("rect", xmin = 3.5, xmax = 6.5, ymin = 0, ymax = 100, 
           fill = "#51C168", alpha = 0.1) +
## Add vertical green line at start of COVID
geom_vline(xintercept = 3.5, color = "#51C168", linetype = "dashed", size = 1) +
geom_line(size = 1.5, alpha = 0.8) +
geom_point(data = data |> group_by(Category, Age, year) |> filter(sort_num == min(sort_num)), 
    size = 2.5, alpha = 0.9) +
facet_wrap(~Category) +
scale_color_manual(values = c("#51C168", "#5C57D8", "#FABA09")) +
ylim(0, 100) +
labs(title = "COVID-19 Impact on Age Groups", 
x = "School Year (Season–Year)", 
y = "% Meeting / Exceeding") +
theme_minimal() +
theme(
axis.text.x = element_text(angle = 90, size = 9),
strip.text = element_text(face = "bold"),
legend.position = "bottom",
plot.caption = element_text(hjust = 0, color = "#51C168", face = "italic")
  )

#Save Png
ggsave("covid_clear_plot.png", covid_plot, width = 20, height = 12, dpi = 300)
covid_plot
```

<img src="proposal_files/figure-gfm/unnamed-chunk-1-1.png" alt="This faceted line chart tracks the percentage of children meeting learning goals across six specific developmental categories: Cognitive, Language, Literacy, Mathematics, Physical, and Social-Emotional. The data covers the 2018–2019 to 2024–2025 school years and organizes time by season: Fall (F), Winter (W) and Spring (S) to highlight progress throughout each year. Each colored line represents a different age group:  Blue is 2–3 years, Pink is 3–4 years and Yellow is 4–5 years. The purpose of this chart is to visualize how the COVID-19 pandemic disrupted learning in these specific areas and to track how children's development has recovered over time."  />

Our age group plot here examines how children of different age groups
were impacted by COVID-19 across six developmental categories. It tracks
their trajectory from pre-pandemic baselines through the recovery
period. During the pandemic, performance became notably unstable , with
the youngest group (ages 2–3) often maintaining higher scores while the
older groups (3–5 years) struggled to maintain consistency. After the
initial lockdown period, we observed specific declines, most notably a
delayed drop for the 2–3 year olds in Social-Emotional and Language
skills around 2021, though the gap between age groups in areas like
Mathematics and Cognitive development often widened with the oldest
children trailing behind. Even four years after the height of the
pandemic, these performance stratifications persist, showing that the
2–3 year olds have largely rebounded to become the highest-performing
group while the 4–5 year olds continue to lag. This shows that while
COVID-19 disrupted learning for everyone, the recovery has been
irregular with the oldest preschool cohort facing the most difficulty in
fully returning to pre-pandemic performance benchmarks.

``` r
# filter 0-1 age group and calculate percentages
data <- general_data_table |>
filter(Age != "0-1") |>
drop_na() |>
group_by(year, Category, Age) |>
summarise(percent = sum(`# Meeting / Exceeding`) / sum(`# Children`) * 100, .groups = "drop") |>
mutate( covid_period = case_when(
year == "2019" ~ "Before COVID",
year %in% c("2021", "2022") ~ "During COVID",
TRUE ~ "After COVID"
  ),
covid_period = factor(covid_period, levels = c("Before COVID", "During COVID", "After COVID"))
)
```

``` r
all_year <- general_data_table |>
  mutate(IEP = na_if(IEP, "N/A")) |>
  filter(!is.na(IEP))

IEP_data <- all_year |>
  mutate(is_fall = (`season` == "Fall"))

IEP_data <- IEP_data |>
  group_by(Category, label, sort_num, is_fall, IEP) |>
  summarise(
    `Avg IEP Meeting Exceeding` = mean(`% Meeting / Exceeding`, na.rm = TRUE),
    .groups = "drop"
  )

iep_graph <- ggplot(
  IEP_data,
  aes(x = `label`, y = `Avg IEP Meeting Exceeding`, fill = IEP, group = IEP)
) +
  geom_area(position = "identity", alpha = 0.4) +
  geom_line(aes(color = IEP), size = 1) +
  geom_point(aes(size = ifelse(is_fall, 4, NA)), shape = 21 , stroke = 0) +
  geom_vline(xintercept = "Fall 21-22") +
  geom_text( 
    aes(x = "Spring 22-23", y = 110, label = "Post-COVID19"),
    size = 1.5) +
  geom_text( 
    aes(x = "Winter 20-21", y = 110, label = "During-COVID19"),
    size = 1.5) +
  facet_wrap(~ Category) +
  labs(
    title = "Academic Performances by Different IEP status During and Post COVID-19",
    x = "School Year (Season–Year)",
    y = "% Meeting / Exceeding",
    subtitle = "Grouped by Category ",
    fill = "IEP Status",
    color = "IEP Status"
  ) +
  scale_size_identity(guide = "none") +
  scale_color_manual(values = c("#51C168", "#5C57D8", "#FABA09"))+
  scale_color_manual(
    values = c(
      "No" = "lightsalmon", 
      "Yes" = "seagreen3"
    ) 
  ) +
  scale_fill_manual(
     values = c(
      "No" = "lightsalmon", 
      "Yes" = "seagreen3"
    ) 
  ) +
  theme_minimal() +
  theme(
    axis.text.x = element_text(angle = 90, hjust = 1),
    legend.position = "bottom",
    strip.text = element_text(face = "bold")
  )
```

    ## Scale for colour is already present.
    ## Adding another scale for colour, which will replace the existing scale.

``` r
iep_graph
```

    ## Warning: Removed 120 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](proposal_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
ggsave("iep_impact.png", iep_graph, width = 15, height = 10, dpi = 300)
```

    ## Warning: Removed 120 rows containing missing values or values outside the scale range
    ## (`geom_point()`).
