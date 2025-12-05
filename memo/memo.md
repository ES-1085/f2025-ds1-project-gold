Project memo
================
Gold Analysts - Mekkawy, Nisan, Razvan

``` r
library(tidyverse)
library(broom)
library(readxl)
library(dplyr)
library(skimr)
```

``` r
X2018_2019 <- read_excel("../data/ignore/2018-2019.xlsx")
X2020_2021 <- read_excel("../data/ignore/2020-2021.xlsx")
X2021_2022 <- read_excel("../data/ignore/2021-2022.xlsx")
X2022_2023 <- read_excel("../data/ignore/2022-2023.xlsx")
X2023_2024 <- read_excel("../data/ignore/2023-2024.xlsx")
X2024_2025 <- read_excel("../data/ignore/2024-2025.xlsx")
```

## Cleaning the imported data and ordering it chronologically

### Step 1: Convert chars into numbers

``` r
#for each year we need to first convert our number of children, number of meeting/exceeding, and percentage of meeting/exceeding in numeric values and create a year column that would help us with sorting and labeling
general_data_table <- bind_rows(
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

### Step 2: Redo label

``` r
general_data_table <- general_data_table |>
  mutate(
    season = case_when(
      str_detect(`Time Period`, "Fall") ~ "Fall",
      str_detect(`Time Period`, "Winter") ~ "Winter",
      str_detect(`Time Period`, "Spring") ~ "Spring"
    ),
    label = paste(season, year),
    #sorting for chronological order taking the beginning of the school year and the code for each season (Fall - 1, Winter - 2, Spring - 3)
    #e.g. Fall 2018-2019 -> 181, Winter 2021-2022 -> 212
    sort_num = as.numeric(str_sub(year, 1, 2)) * 10 + match(season,c("Fall","Winter","Spring")))
```

### Step 3: Order data chronologically

``` r
general_data_table <- general_data_table |>
  mutate(
    label = fct_reorder(label, sort_num)
  )
```

## Plots

### Plot 1: Average performance

#### First General Data Attempt

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

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](memo_files/figure-gfm/first-general-graph-attempt-1.png)<!-- -->

``` r
#saving
ggsave("general_plot.png", general_data_plot, width = 10, height = 20, dpi = 300)
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

``` r
#creating a new column that would help us highlight the beginning of the school year
average_general_data_table <- general_data_table |>
  mutate(is_fall = (`season` == "Fall"))
```

``` r
#calculating the average of all age groups' seasonal performance
average_general_data_table <- average_general_data_table |>
  group_by(Category, label, sort_num, is_fall) |>
  summarise(
    `Avg Meeting Exceeding` = mean(`% Meeting / Exceeding`, na.rm = TRUE),
    .groups = "drop"
  )
```

#### Final Plot 1

``` r
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

![](memo_files/figure-gfm/final-general-graph-1.png)<!-- -->

``` r
#saving
ggsave("average_general_plot.png", average_general_data_plot, width = 15, height = 10, dpi = 300)
```

    ## Warning: Removed 72 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

### Plot 2: IEP

Before startign work on IEP graph, we have crated another dataset using
general_data_table. To create the IEP_data we first mutate datasets that
has N/A as IPE, and then we have calculated the mean % Meeting /
Exceeding for eahc trimester in every year.

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
```

After creating IEP data, we have created a

``` r
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

iep_graph
```

    ## Warning: Removed 120 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](memo_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggsave("iep_impact.png", iep_graph, width = 15, height = 10, dpi = 300)
```

    ## Warning: Removed 120 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

### Plot 3: \_\_\_\_\_\_\_\_\_\_\_

Add more plot sections as needed. Each project should have at least 3
plots, but talk to me if you have fewer than 3.

### Plot 4: \_\_\_\_\_\_\_\_\_\_\_
