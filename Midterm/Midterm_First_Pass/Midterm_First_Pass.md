---
title: "Midterm_First_Pass"
author: "Hannah Houts"
date: "March 3, 2019"
output: 
  html_document:
    keep_md: yes
    theme: spacelab
    toc: no
    toc_float: no
  pdf_document:
    toc: yes
---
### Note:
I didnt have the chance to try this our in class, because I was nose deep in grad school interviews. I'm going to give it a fair chance (45 minutes), and upload those results. Then I'll copy what I have, correct/finish the test, and upload it seperately. 


## Instructions
This exam is designed to show me what you have learned and where there are problems. You may use your notes and anything from the `class_files` folder, but please no internet searches. You have 35 minutes to complete as many of these exercises as possible on your own, and 10 minutes to work with a partner.  

At the end of the exam, upload the complete .Rmd file to your GitHub repository.  

1. (1 point) Load the tidyverse.

```r
library(tidyverse)
```

```
## -- Attaching packages ------------------------------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0       v purrr   0.2.5  
## v tibble  2.0.1       v dplyr   0.8.0.1
## v tidyr   0.8.2       v stringr 1.3.1  
## v readr   1.3.1       v forcats 0.3.0
```

```
## -- Conflicts ---------------------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

2. (2 points) For these questions, we will use data about California colleges. Load the `ca_college_data.csv` as a new object called `colleges`.


```r
colleges <- readr::read_csv("./../../data/ca_college_data.csv")
```

```
## Parsed with column specification:
## cols(
##   INSTNM = col_character(),
##   CITY = col_character(),
##   STABBR = col_character(),
##   ZIP = col_character(),
##   ADM_RATE = col_double(),
##   SAT_AVG = col_double(),
##   PCIP26 = col_double(),
##   COSTT4_A = col_double(),
##   C150_4_POOLED = col_double(),
##   PFTFTUG1_EF = col_double()
## )
```

3. (1 point) Use your preferred function to have a look at the data and get an idea of its structure.

```r
head(colleges)
```

```
## # A tibble: 6 x 10
##   INSTNM CITY  STABBR ZIP   ADM_RATE SAT_AVG PCIP26 COSTT4_A C150_4_POOLED
##   <chr>  <chr> <chr>  <chr>    <dbl>   <dbl>  <dbl>    <dbl>         <dbl>
## 1 Gross~ El C~ CA     9202~       NA      NA 0.0016     7956            NA
## 2 Colle~ Visa~ CA     9327~       NA      NA 0.0066     8109            NA
## 3 Colle~ San ~ CA     9440~       NA      NA 0.0038     8278            NA
## 4 Ventu~ Vent~ CA     9300~       NA      NA 0.0035     8407            NA
## 5 Oxnar~ Oxna~ CA     9303~       NA      NA 0.0085     8516            NA
## 6 Moorp~ Moor~ CA     9302~       NA      NA 0.0151     8577            NA
## # ... with 1 more variable: PFTFTUG1_EF <dbl>
```

```r
glimpse(colleges)
```

```
## Observations: 341
## Variables: 10
## $ INSTNM        <chr> "Grossmont College", "College of the Sequoias", ...
## $ CITY          <chr> "El Cajon", "Visalia", "San Mateo", "Ventura", "...
## $ STABBR        <chr> "CA", "CA", "CA", "CA", "CA", "CA", "CA", "CA", ...
## $ ZIP           <chr> "92020-1799", "93277-2214", "94402-3784", "93003...
## $ ADM_RATE      <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ...
## $ SAT_AVG       <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ...
## $ PCIP26        <dbl> 0.0016, 0.0066, 0.0038, 0.0035, 0.0085, 0.0151, ...
## $ COSTT4_A      <dbl> 7956, 8109, 8278, 8407, 8516, 8577, 8580, 9181, ...
## $ C150_4_POOLED <dbl> NA, NA, NA, NA, NA, NA, 0.2334, NA, NA, NA, NA, ...
## $ PFTFTUG1_EF   <dbl> 0.3546, 0.5413, 0.3567, 0.3824, 0.2753, 0.4286, ...
```


4. (1 point) What are the column names?


```r
colnames(colleges)
```

```
##  [1] "INSTNM"        "CITY"          "STABBR"        "ZIP"          
##  [5] "ADM_RATE"      "SAT_AVG"       "PCIP26"        "COSTT4_A"     
##  [9] "C150_4_POOLED" "PFTFTUG1_EF"
```

5. (3 points) Are there any NA's in the data? If so, how many are present and in which variables?


```r
#install.packages("skimr")
library("skimr")
```

```
## 
## Attaching package: 'skimr'
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```r
colleges %>% 
  skimr::skim()
```

```
## Skim summary statistics
##  n obs: 341 
##  n variables: 10 
## 
## -- Variable type:character ---------------------------------------------------------------------------------------------------------------------------------------------
##  variable missing complete   n min max empty n_unique
##      CITY       0      341 341   4  19     0      161
##    INSTNM       0      341 341  10  63     0      341
##    STABBR       0      341 341   2   2     0        3
##       ZIP       0      341 341   5  10     0      324
## 
## -- Variable type:numeric -----------------------------------------------------------------------------------------------------------------------------------------------
##       variable missing complete   n     mean        sd        p0      p25
##       ADM_RATE     240      101 341     0.59     0.23     0.081      0.46
##  C150_4_POOLED     221      120 341     0.57     0.21     0.062      0.43
##       COSTT4_A     124      217 341 26685.17 18122.7   7956      12578   
##         PCIP26      35      306 341     0.02     0.038    0          0   
##    PFTFTUG1_EF      53      288 341     0.56     0.29     0.0064     0.32
##        SAT_AVG     276       65 341  1112.31   170.8    870        985   
##       p50       p75     p100     hist
##      0.64     0.75      1    <U+2583><U+2582><U+2585><U+2587><U+2586><U+2587><U+2585><U+2583>
##      0.58     0.72      0.96 <U+2581><U+2583><U+2583><U+2586><U+2587><U+2587><U+2583><U+2585>
##  16591    39289     69355    <U+2587><U+2583><U+2581><U+2582><U+2581><U+2581><U+2581><U+2581>
##      0        0.025     0.22 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##      0.5      0.81      1    <U+2581><U+2585><U+2587><U+2586><U+2583><U+2585><U+2583><U+2587>
##   1078     1237      1555    <U+2586><U+2587><U+2585><U+2583><U+2583><U+2582><U+2582><U+2581>
```

The number on NAs per column(variable) is shown above, under name _Variable type:numeric : missing_
Each variable has some NAs for a total of 949 NAs

6. (3 points) Which cities in California have the highest number of colleges?


```r
    colleges %>%
        group_by(CITY) %>%
            summarize(total_count=n())%>%
                arrange(desc(total_count))
```

```
## # A tibble: 161 x 2
##    CITY          total_count
##    <chr>               <int>
##  1 Los Angeles            24
##  2 San Diego              18
##  3 San Francisco          15
##  4 Sacramento             10
##  5 Berkeley                9
##  6 Oakland                 9
##  7 Claremont               7
##  8 Pasadena                6
##  9 Fresno                  5
## 10 Irvine                  5
## # ... with 151 more rows
```
Los Angeles, San Diego & San Francisco


7. (4 points) The column `COSTT4_A` is the annual cost of each institution. Which city has the highest cost?

```r
    colleges %>%
        group_by(CITY) %>%
            filter(!is.na(COSTT4_A)) %>%
            summarize( mean_cost = mean(COSTT4_A),
                       max_cost = max(COSTT4_A)) %>%
                arrange(desc(max_cost))
```

```
## # A tibble: 132 x 3
##    CITY          mean_cost max_cost
##    <chr>             <dbl>    <dbl>
##  1 Claremont        66498     69355
##  2 Los Angeles      40796.    67225
##  3 Malibu           66152     66152
##  4 San Francisco    43700.    65453
##  5 Valencia         64686     64686
##  6 Orange           64501     64501
##  7 Pasadena         45616.    63471
##  8 Santa Clara      39008     62964
##  9 Redlands         61542     61542
## 10 Moraga           61095     61095
## # ... with 122 more rows
```
Cities with the most expensive schools: Claremont, Los Angeles, and Malibu


```r
   colleges %>%
        group_by(CITY) %>%
            filter(!is.na(COSTT4_A)) %>%
            summarize( mean_cost = mean(COSTT4_A),
                       max_cost = max(COSTT4_A)) %>%
                arrange(desc(mean_cost))
```

```
## # A tibble: 132 x 3
##    CITY                mean_cost max_cost
##    <chr>                   <dbl>    <dbl>
##  1 Claremont               66498    69355
##  2 Malibu                  66152    66152
##  3 Valencia                64686    64686
##  4 Orange                  64501    64501
##  5 Redlands                61542    61542
##  6 Moraga                  61095    61095
##  7 Atherton                56035    56035
##  8 Thousand Oaks           54373    54373
##  9 Rancho Palos Verdes     50758    50758
## 10 La Verne                50603    50603
## # ... with 122 more rows
```
Cities with the most expensive average tuition: Claremont, Malibu, and Valencia


## This is as far as I got in 45 minutes. 


8. (3 points) The column `ADM_RATE` is the admissions rate by college and `C150_4_POOLED` is the four-year completion rate. Use a scatterplot to show the relationship between these two variables. What does this mean?

9. (1 point) The column titled `INSTNM` is the institution name. We are only interested in the University of California colleges. Run the code below and look at the output. Are all of the columns tidy? Why or why not?

```r
#univ_calif <- 
#  colleges %>% 
#  filter_all(any_vars(str_detect(., pattern = "University of California")))
#univ_calif
```

10. (2 points)Use `separate()` to separate institution name into two new columns "UNIV" and "CAMPUS".

11. (1 point) As a final step, remove `Hastings College of Law` and `UC San Francisco` and store the final data frame as a new object `univ_calif_final`.

12. (3 points) The column `ADM_RATE` is the admissions rate by campus. Which UC has the lowest and highest admissions rates? Please use a barplot.

## Knit Your Output and Post to [GitHub](https://github.com/FRS417-DataScienceBiologists)
