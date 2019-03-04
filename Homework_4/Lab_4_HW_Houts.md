---
title: "HW_4_Houts"
author: "Hannah Houts"
date: "February 25, 2019"
output: 
  html_document:
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our [GitHub repository](https://github.com/FRS417-DataScienceBiologists). I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Life History
Aren't mammals fun? Let's load up some more mammal data. This will be life history data for mammals. The [data](http://esapubs.org/archive/ecol/E084/093/) are from: *S. K. Morgan Ernest. 2003. Life history characteristics of placental non-volant mammals. Ecology 84:3402.*  


```r
life_history <- readr::read_csv("./../data/mammal_lifehistories_v2.csv")
```

```
## Parsed with column specification:
## cols(
##   order = col_character(),
##   family = col_character(),
##   Genus = col_character(),
##   species = col_character(),
##   mass = col_double(),
##   gestation = col_double(),
##   newborn = col_double(),
##   weaning = col_double(),
##   `wean mass` = col_double(),
##   AFR = col_double(),
##   `max. life` = col_double(),
##   `litter size` = col_double(),
##   `litters/year` = col_double()
## )
```

```r
msleep <- msleep
```

Rename some of the variables. Notice that I am replacing the old `life_history` data.

```r
life_history <- 
  life_history %>% 
  dplyr::rename(
          genus        = Genus,
          wean_mass    = `wean mass`,
          max_life     = `max. life`,
          litter_size  = `litter size`,
          litters_yr   = `litters/year`
          )
```

1. Explore the data using the method that you prefer. Below, I am using a new package called `skimr`. If you want to use this, make sure that it is installed.



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
life_history %>% 
  skimr::skim()
```

```
## Skim summary statistics
##  n obs: 1440 
##  n variables: 13 
## 
## -- Variable type:character ---------------------------------------------------------------------------------------------------------------------------------------------
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## -- Variable type:numeric -----------------------------------------------------------------------------------------------------------------------------------------------
##     variable missing complete    n      mean         sd   p0  p25     p50
##          AFR       0     1440 1440   -408.12     504.97 -999 -999    2.5 
##    gestation       0     1440 1440   -287.25     455.36 -999 -999    1.05
##  litter_size       0     1440 1440    -55.63     234.88 -999    1    2.27
##   litters_yr       0     1440 1440   -477.14     500.03 -999 -999    0.38
##         mass       0     1440 1440 383576.72 5055162.92 -999   50  403.02
##     max_life       0     1440 1440   -490.26     615.3  -999 -999 -999   
##      newborn       0     1440 1440   6703.15   90912.52 -999 -999    2.65
##    wean_mass       0     1440 1440  16048.93   5e+05    -999 -999 -999   
##      weaning       0     1440 1440   -427.17     496.71 -999 -999    0.73
##      p75          p100     hist
##    15.61     210       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587><U+2581>
##     4.5       21.46    <U+2583><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     3.83      14.18    <U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     1.15       7.5     <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##  7009.17       1.5e+08 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##   147.25    1368       <U+2587><U+2581><U+2581><U+2583><U+2582><U+2581><U+2581><U+2581>
##    98    2250000       <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##    10          1.9e+07 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##     2         48       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
```

2. Run the code below. Are there any NA's in the data? Does this seem likely?

```r
life_history %>% 
  summarize(number_nas= sum(is.na(life_history)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1          0
```
According to the function, there are no "NA's" in the data. This is unlikely, they are probably saved as something other than "NA"



3. Are there any missing data (NA's) represented by different values? How much and where? In which variables do we have the most missing data? Can you think of a reason why so much data are missing in this variable?
NA's are represented by -999. The weaning mass has the most NAs. This is because it may be difficult to weigh some of these animals at weaning, because theyre wild animals. 


4. Compared to the `msleep` data, we have better representation among taxa. Produce a summary that shows the number of observations by taxonomic order.

```r
life_history %>%
  group_by(order) %>%
  summarize(count=n())
```

```
## # A tibble: 17 x 2
##    order          count
##    <chr>          <int>
##  1 Artiodactyla     161
##  2 Carnivora        197
##  3 Cetacea           55
##  4 Dermoptera         2
##  5 Hyracoidea         4
##  6 Insectivora       91
##  7 Lagomorpha        42
##  8 Macroscelidea     10
##  9 Perissodactyla    15
## 10 Pholidota          7
## 11 Primates         156
## 12 Proboscidea        2
## 13 Rodentia         665
## 14 Scandentia         7
## 15 Sirenia            5
## 16 Tubulidentata      1
## 17 Xenarthra         20
```

```r
#msleep %>%
#  group_by(vore) %>% #we are grouping by feeding ecology
#  summarize(min_bodywt=min(bodywt),
#            max_bodywt=max(bodywt),
#            mean_bodywt=mean(bodywt),
#            total=n())
```


5. Mammals have a range of life histories, including lifespan. Produce a summary of lifespan in years by order. Be sure to include the minimum, maximum, mean, standard deviation, and total n.

```r
#adjusts "-999" values to r-readable NAs, only pass in the data table
life_history <- na_if(life_history,"-999")


life_history %>%
    group_by(order) %>% 
    filter(!is.na(max_life)) %>%
    summarize(min_lifespan=min(max_life),
              max_lifespan=max(max_life),
              mean_lifespan=mean(max_life),
              total_count=n()
            )
```

```
## # A tibble: 17 x 5
##    order          min_lifespan max_lifespan mean_lifespan total_count
##    <chr>                 <dbl>        <dbl>         <dbl>       <int>
##  1 Artiodactyla             81          732         248.           99
##  2 Carnivora                60          672         253.          138
##  3 Cetacea                 156         1368         586.           39
##  4 Dermoptera              210          210         210             1
##  5 Hyracoidea              132          147         140.            2
##  6 Insectivora              14          156          46.2          40
##  7 Lagomorpha               72          216         108.            8
##  8 Macroscelidea            36          105          68.2           4
##  9 Perissodactyla          252          600         426.           12
## 10 Pholidota               240          240         240             1
## 11 Primates                106          726         309.           74
## 12 Proboscidea             840          960         900             2
## 13 Rodentia                 12          420          83.8         161
## 14 Scandentia               32          149         106.            3
## 15 Sirenia                 150          876         518             3
## 16 Tubulidentata           288          288         288             1
## 17 Xenarthra               108          480         255.           11
```

6. Let's look closely at gestation and newborns. Summarize the mean gestation, newborn mass, and weaning mass by order. Add a new column that shows mean gestation in years and sort in descending order. Which group has the longest mean gestation? What is the common name for these mammals?


```r
life_history %>%
    filter(!is.na(gestation), !is.na(newborn), !is.na(wean_mass)) %>%
    group_by(order) %>% 
  
    summarize(mean_gestation = mean(gestation),
              mean_newborn_mass = mean(newborn),
              mean_weaning_mass = mean(wean_mass),
              mean_gestation_years = (mean_gestation/12)) %>%
  
              arrange(desc(mean_gestation_years))
```

```
## # A tibble: 16 x 5
##    order  mean_gestation mean_newborn_ma~ mean_weaning_ma~ mean_gestation_~
##    <chr>           <dbl>            <dbl>            <dbl>            <dbl>
##  1 Probo~          21.5          99006.           600000             1.79  
##  2 Peris~          13.9          31971.           382191.            1.16  
##  3 Cetac~          11.2         569104.          4796125             0.933 
##  4 Siren~          10.2          12500             67500             0.854 
##  5 Hyrac~           7.44           232.              500             0.62  
##  6 Artio~           7.34          8639.            51025.            0.612 
##  7 Tubul~           7.08          1734              6250             0.59  
##  8 Prima~           5.79           429.             2156.            0.482 
##  9 Carni~           4.52          5123.            21286.            0.376 
## 10 Pholi~           4.31           229               812.            0.360 
## 11 Xenar~           2.09           105               420             0.174 
## 12 Scand~           1.68            16.5             102.            0.140 
## 13 Macro~           1.66            45.4             104.            0.139 
## 14 Lagom~           1.27            70.8             715.            0.106 
## 15 Roden~           1.15            28.4             153.            0.0957
## 16 Insec~           1.00             4.10             40.3           0.0835
```
Which group has the longest mean gestation? 
Proboscidea

What is the common name for these mammals?
Elephants!



## Push your final code to [GitHub](https://github.com/FRS417-DataScienceBiologists)
Make sure that you push your code into the appropriate folder. Also, be sure that you have check the `keep md` file in the knit preferences.


