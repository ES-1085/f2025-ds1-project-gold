README
================
Gold Analysts - Mekkawy, Nissan, Razvan

# data

Data file(s) placed in this folder.

``` r
library(readxl)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
X2018_2019 <- read_excel("../data/ignore/2018-2019.xlsx")
X2020_2021 <- read_excel("../data/ignore/2020-2021.xlsx")
X2021_2022 <- read_excel("../data/ignore/2021-2022.xlsx")
X2022_2023 <- read_excel("../data/ignore/2022-2023.xlsx")
X2023_2024 <- read_excel("../data/ignore/2023-2024.xlsx")
X2024_2025 <- read_excel("../data/ignore/2024-2025.xlsx")
```

## 2018-2019

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2018-2019, Winter
  2018-2019, Spring 2018-2019)

``` r
ls(X2018_2019)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2018_2019)
```

    ## Rows: 90
    ## Columns: 7
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `# Children`            <dbl> 1, 2, 17, 71, 294, 1, 2, 17, 71, 297, 1, 2, 17…
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "4-5", "0-1", "1-2…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "N/A", "N/A", "N/A", "N/A…
    ## $ `# Meeting / Exceeding` <dbl> 1, 2, 14, 38, 96, 1, 2, 17, 61, 141, 1, 1, 15,…
    ## $ `% Meeting / Exceeding` <dbl> 100.00000, 100.00000, 82.35294, 53.52113, 32.6…
    ## $ `Time Period`           <chr> "Fall 2018/2019", "Fall 2018/2019", "Fall 2018…

## 2020-2021

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2020-2021, Winter
  2020-2021, Spring 2020-2021)

``` r
ls(X2020_2021)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2020_2021)
```

    ## Rows: 126
    ## Columns: 7
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `# Children`            <dbl> 2, 7, 15, 7, 19, 30, 65, 2, 7, 16, 8, 21, 30, …
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "4-5", "3-4", "4-5…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "Yes", "Yes", "No", "No",…
    ## $ `# Meeting / Exceeding` <dbl> 2, 5, 10, 5, 8, 26, 48, 2, 6, 15, 7, 15, 28, 5…
    ## $ `% Meeting / Exceeding` <dbl> 100.00000, 71.42857, 66.66667, 71.42857, 42.10…
    ## $ `Time Period`           <chr> "Fall 2020/2021", "Fall 2020/2021", "Fall 2020…

## 2021-2022

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2021-2022, Winter
  2021-2022, Spring 2021-2022)

``` r
ls(X2021_2022)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2021_2022)
```

    ## Rows: 108
    ## Columns: 7
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `# Children`            <chr> "2.0", "3.0", "13.0", "41.0", "N/A", "N/A", "2…
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "4-5", "4-5", "0-1…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "N/A", "No", "Yes", "N/A"…
    ## $ `# Meeting / Exceeding` <chr> "2.0", "3.0", "8.0", "35", "N/A", "N/A", "2.0"…
    ## $ `% Meeting / Exceeding` <dbl> 100.0, 100.0, 61.5, 85.4, 76.0, 45.0, 100.0, 1…
    ## $ `Time Period`           <chr> "Fall 2021/2022", "Fall 2021/2022", "Fall 2021…

## 2022-2023

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2022-2023, Winter
  2022-2023, Spring 2022-2023)

``` r
ls(X2022_2023)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2022_2023)
```

    ## Rows: 126
    ## Columns: 7
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `# Children`            <dbl> 9, 15, 9, 13, 30, 22, 89, 9, 15, 9, 13, 30, 23…
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "3-4", "4-5", "4-5…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "Yes", "No", "Yes", "No",…
    ## $ `# Meeting / Exceeding` <dbl> 9, 10, 6, 6, 25, 6, 53, 7, 13, 9, 9, 29, 10, 7…
    ## $ `% Meeting / Exceeding` <dbl> 100.0, 66.7, 66.7, 46.2, 83.3, 27.3, 59.5, 77.…
    ## $ `Time Period`           <chr> "Fall 2022/2023", "Fall 2022/2023", "Fall 2022…

## 2023-2024

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2023-2024, Winter
  2023-2024, Spring 2023-2024)

``` r
ls(X2023_2024)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2023_2024)
```

    ## Rows: 126
    ## Columns: 7
    ## $ Category                <chr> "Social-Emotional", "Social-Emotional", "Socia…
    ## $ `# Children`            <dbl> 0, 11, 27, 13, 30, 22, 89, 0, 11, 27, 13, 30, …
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "3-4", "4-5", "4-5…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "Yes", "No", "Yes", "No",…
    ## $ `# Meeting / Exceeding` <dbl> 0, 10, 18, 6, 25, 6, 53, 0, 11, 22, 9, 29, 10,…
    ## $ `% Meeting / Exceeding` <dbl> 0.00000, 90.90909, 66.66667, 46.15385, 83.3333…
    ## $ `Time Period`           <chr> "Fall 2022/2023", "Fall 2022/2023", "Fall 2022…

## 2024-2025

- `Category`: 6 categories analyzed: Social-Emotional, Physical,
  Language, Cognitive, Literacy, Mathematics
- `# Children`: Total \# of children assessed in each age group
- `Age`: 5 age groups analyzed: 0-1, 1-2, 2-3, 3-4, 4-5
- `IEP`: IEP status: N/A (0-1, 1-2, 2-3 and some 3-4, 4-5 depending on
  the year), Yes or No (most 3-4 and 4-5)
- `# Meeting/Exceeding` : \# of children meeting or exceeding
  expectations
- `% Meeting/Exceeding` : % of children meeting or exceeding
  expectations
- `Time Period` : trimester and year analyzed (Fall 2024-2025, Winter
  2024-2025, Spring 2024-2025)

``` r
ls(X2024_2025)
```

    ## [1] "# Children"            "# Meeting / Exceeding" "% Meeting / Exceeding"
    ## [4] "Age"                   "Category"              "IEP"                  
    ## [7] "Time Period"

``` r
glimpse(X2024_2025)
```

    ## Rows: 126
    ## Columns: 7
    ## $ Category                <chr> "Cognitive", "Cognitive", "Cognitive", "Cognit…
    ## $ `# Children`            <dbl> 12, 16, 40, 56, 16, 99, 21, 12, 16, 40, 56, 16…
    ## $ Age                     <chr> "0-1", "1-2", "2-3", "3-4", "3-4", "4-5", "4-5…
    ## $ IEP                     <chr> "N/A", "N/A", "N/A", "No", "Yes", "No", "Yes",…
    ## $ `# Meeting / Exceeding` <dbl> 12, 14, 34, 44, 7, 72, 10, 12, 10, 32, 38, 3, …
    ## $ `% Meeting / Exceeding` <dbl> 100.00000, 87.50000, 85.00000, 78.57143, 43.75…
    ## $ `Time Period`           <chr> "Fall 2024/2025", "Fall 2024/2025", "Fall 2024…
