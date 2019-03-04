---
title: "Lab3_HW"
author: "Hannah Houts"
date: "Winter 2019"
output: 
  html_document:
    keep_md: yes
    theme: spacelab
---

##Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our GitHub repository. I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.

Load the libraries

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

For this assignment we are going to work with a large dataset from the United Nations Food and Agriculture Organization on world fisheries. The data are messy, so for this assignment I am going to provide some help. The code I use will likely be useful in the future so keep it handy. First, load the data. Read the error message.


```r
fisheries <- read_csv("./../data/FAO_1950to2012_111914.csv")
```

```
## Warning: Duplicated column names deduplicated: 'Species (ISSCAAP group)'
## => 'Species (ISSCAAP group)_1' [4], 'Species (ASFIS species)' => 'Species
## (ASFIS species)_1' [5], 'Species (ASFIS species)' => 'Species (ASFIS
## species)_2' [6]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `Species (ISSCAAP group)` = col_double(),
##   `Fishing area (FAO major fishing area)` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

```r
head(fisheries)
```

```
## # A tibble: 6 x 71
##   `Country (Count~ `Species (ASFIS~ `Species (ISSCA~ `Species (ISSCA~
##   <chr>            <chr>                       <dbl> <chr>           
## 1 Albania          Angelsharks, sa~               38 Sharks, rays, c~
## 2 Albania          Atlantic bonito                36 Tunas, bonitos,~
## 3 Albania          Barracudas nei                 37 Miscellaneous p~
## 4 Albania          Blue and red sh~               45 Shrimps, prawns 
## 5 Albania          Blue whiting(=P~               32 Cods, hakes, ha~
## 6 Albania          Bluefish                       37 Miscellaneous p~
## # ... with 67 more variables: `Species (ASFIS species)_1` <chr>, `Species
## #   (ASFIS species)_2` <chr>, `Fishing area (FAO major fishing
## #   area)` <dbl>, `Measure (Measure)` <chr>, `1950` <chr>, `1951` <chr>,
## #   `1952` <chr>, `1953` <chr>, `1954` <chr>, `1955` <chr>, `1956` <chr>,
## #   `1957` <chr>, `1958` <chr>, `1959` <chr>, `1960` <chr>, `1961` <chr>,
## #   `1962` <chr>, `1963` <chr>, `1964` <chr>, `1965` <chr>, `1966` <chr>,
## #   `1967` <chr>, `1968` <chr>, `1969` <chr>, `1970` <chr>, `1971` <chr>,
## #   `1972` <chr>, `1973` <chr>, `1974` <chr>, `1975` <chr>, `1976` <chr>,
## #   `1977` <chr>, `1978` <chr>, `1979` <chr>, `1980` <chr>, `1981` <chr>,
## #   `1982` <chr>, `1983` <chr>, `1984` <chr>, `1985` <chr>, `1986` <chr>,
## #   `1987` <chr>, `1988` <chr>, `1989` <chr>, `1990` <chr>, `1991` <chr>,
## #   `1992` <chr>, `1993` <chr>, `1994` <chr>, `1995` <chr>, `1996` <chr>,
## #   `1997` <chr>, `1998` <chr>, `1999` <chr>, `2000` <chr>, `2001` <chr>,
## #   `2002` <chr>, `2003` <chr>, `2004` <chr>, `2005` <chr>, `2006` <chr>,
## #   `2007` <chr>, `2008` <chr>, `2009` <chr>, `2010` <chr>, `2011` <chr>,
## #   `2012` <chr>
```

1. Do you see any potential problems with the column names? Does the error message now make more sense?
_Column names are duplicated so R manipulated them to unique names_

2. The make.names() command is helpful when there are issues with column names. Notice that although the names are still cumbersome, much of the problemtatic syntax is removed.

3. Let's rename the columns. Use rename() to adjust the names as follows. Double check to make sure the rename worked correctly. Make sure to replace the old fisheries object with a new one so you can keep the column names.


```r
names(fisheries) = make.names(names(fisheries), unique=T) 
#changes the column names
names(fisheries)
```

```
##  [1] "Country..Country."                    
##  [2] "Species..ASFIS.species."              
##  [3] "Species..ISSCAAP.group."              
##  [4] "Species..ISSCAAP.group._1"            
##  [5] "Species..ASFIS.species._1"            
##  [6] "Species..ASFIS.species._2"            
##  [7] "Fishing.area..FAO.major.fishing.area."
##  [8] "Measure..Measure."                    
##  [9] "X1950"                                
## [10] "X1951"                                
## [11] "X1952"                                
## [12] "X1953"                                
## [13] "X1954"                                
## [14] "X1955"                                
## [15] "X1956"                                
## [16] "X1957"                                
## [17] "X1958"                                
## [18] "X1959"                                
## [19] "X1960"                                
## [20] "X1961"                                
## [21] "X1962"                                
## [22] "X1963"                                
## [23] "X1964"                                
## [24] "X1965"                                
## [25] "X1966"                                
## [26] "X1967"                                
## [27] "X1968"                                
## [28] "X1969"                                
## [29] "X1970"                                
## [30] "X1971"                                
## [31] "X1972"                                
## [32] "X1973"                                
## [33] "X1974"                                
## [34] "X1975"                                
## [35] "X1976"                                
## [36] "X1977"                                
## [37] "X1978"                                
## [38] "X1979"                                
## [39] "X1980"                                
## [40] "X1981"                                
## [41] "X1982"                                
## [42] "X1983"                                
## [43] "X1984"                                
## [44] "X1985"                                
## [45] "X1986"                                
## [46] "X1987"                                
## [47] "X1988"                                
## [48] "X1989"                                
## [49] "X1990"                                
## [50] "X1991"                                
## [51] "X1992"                                
## [52] "X1993"                                
## [53] "X1994"                                
## [54] "X1995"                                
## [55] "X1996"                                
## [56] "X1997"                                
## [57] "X1998"                                
## [58] "X1999"                                
## [59] "X2000"                                
## [60] "X2001"                                
## [61] "X2002"                                
## [62] "X2003"                                
## [63] "X2004"                                
## [64] "X2005"                                
## [65] "X2006"                                
## [66] "X2007"                                
## [67] "X2008"                                
## [68] "X2009"                                
## [69] "X2010"                                
## [70] "X2011"                                
## [71] "X2012"
```



```r
head(fisheries)
```

```
## # A tibble: 6 x 71
##   Country..Countr~ Species..ASFIS.~ Species..ISSCAA~ Species..ISSCAA~
##   <chr>            <chr>                       <dbl> <chr>           
## 1 Albania          Angelsharks, sa~               38 Sharks, rays, c~
## 2 Albania          Atlantic bonito                36 Tunas, bonitos,~
## 3 Albania          Barracudas nei                 37 Miscellaneous p~
## 4 Albania          Blue and red sh~               45 Shrimps, prawns 
## 5 Albania          Blue whiting(=P~               32 Cods, hakes, ha~
## 6 Albania          Bluefish                       37 Miscellaneous p~
## # ... with 67 more variables: Species..ASFIS.species._1 <chr>,
## #   Species..ASFIS.species._2 <chr>,
## #   Fishing.area..FAO.major.fishing.area. <dbl>, Measure..Measure. <chr>,
## #   X1950 <chr>, X1951 <chr>, X1952 <chr>, X1953 <chr>, X1954 <chr>,
## #   X1955 <chr>, X1956 <chr>, X1957 <chr>, X1958 <chr>, X1959 <chr>,
## #   X1960 <chr>, X1961 <chr>, X1962 <chr>, X1963 <chr>, X1964 <chr>,
## #   X1965 <chr>, X1966 <chr>, X1967 <chr>, X1968 <chr>, X1969 <chr>,
## #   X1970 <chr>, X1971 <chr>, X1972 <chr>, X1973 <chr>, X1974 <chr>,
## #   X1975 <chr>, X1976 <chr>, X1977 <chr>, X1978 <chr>, X1979 <chr>,
## #   X1980 <chr>, X1981 <chr>, X1982 <chr>, X1983 <chr>, X1984 <chr>,
## #   X1985 <chr>, X1986 <chr>, X1987 <chr>, X1988 <chr>, X1989 <chr>,
## #   X1990 <chr>, X1991 <chr>, X1992 <chr>, X1993 <chr>, X1994 <chr>,
## #   X1995 <chr>, X1996 <chr>, X1997 <chr>, X1998 <chr>, X1999 <chr>,
## #   X2000 <chr>, X2001 <chr>, X2002 <chr>, X2003 <chr>, X2004 <chr>,
## #   X2005 <chr>, X2006 <chr>, X2007 <chr>, X2008 <chr>, X2009 <chr>,
## #   X2010 <chr>, X2011 <chr>, X2012 <chr>
```


```r
fisheries <- fisheries %>% 
                rename(
                  country = Country..Country.,
                      
                  commname = Species..ASFIS.species.,
               
                  spgroup = Species..ISSCAAP.group.,    
              
                  spcode = Species..ASFIS.species._1,  
                  
                  spgroupname = Species..ISSCAAP.group._1,
                  
                  sciname = Species..ASFIS.species._2,
              
                  region = Fishing.area..FAO.major.fishing.area.,
                 
                  unit = Measure..Measure.)

head(fisheries)
```

```
## # A tibble: 6 x 71
##   country commname spgroup spgroupname spcode sciname region unit  X1950
##   <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <chr>
## 1 Albania Angelsh~      38 Sharks, ra~ 10903~ Squati~     37 Quan~ ...  
## 2 Albania Atlanti~      36 Tunas, bon~ 17501~ Sarda ~     37 Quan~ ...  
## 3 Albania Barracu~      37 Miscellane~ 17710~ Sphyra~     37 Quan~ ...  
## 4 Albania Blue an~      45 Shrimps, p~ 22802~ Ariste~     37 Quan~ ...  
## 5 Albania Blue wh~      32 Cods, hake~ 14804~ Microm~     37 Quan~ ...  
## 6 Albania Bluefish      37 Miscellane~ 17020~ Pomato~     37 Quan~ ...  
## # ... with 62 more variables: X1951 <chr>, X1952 <chr>, X1953 <chr>,
## #   X1954 <chr>, X1955 <chr>, X1956 <chr>, X1957 <chr>, X1958 <chr>,
## #   X1959 <chr>, X1960 <chr>, X1961 <chr>, X1962 <chr>, X1963 <chr>,
## #   X1964 <chr>, X1965 <chr>, X1966 <chr>, X1967 <chr>, X1968 <chr>,
## #   X1969 <chr>, X1970 <chr>, X1971 <chr>, X1972 <chr>, X1973 <chr>,
## #   X1974 <chr>, X1975 <chr>, X1976 <chr>, X1977 <chr>, X1978 <chr>,
## #   X1979 <chr>, X1980 <chr>, X1981 <chr>, X1982 <chr>, X1983 <chr>,
## #   X1984 <chr>, X1985 <chr>, X1986 <chr>, X1987 <chr>, X1988 <chr>,
## #   X1989 <chr>, X1990 <chr>, X1991 <chr>, X1992 <chr>, X1993 <chr>,
## #   X1994 <chr>, X1995 <chr>, X1996 <chr>, X1997 <chr>, X1998 <chr>,
## #   X1999 <chr>, X2000 <chr>, X2001 <chr>, X2002 <chr>, X2003 <chr>,
## #   X2004 <chr>, X2005 <chr>, X2006 <chr>, X2007 <chr>, X2008 <chr>,
## #   X2009 <chr>, X2010 <chr>, X2011 <chr>, X2012 <chr>
```

4. Are these data tidy? Why or why not, and, how do you know?
 _No, because year is stored in multiple columns. Year should be one column._

5. We need to tidy the data using gather(). The code below will not run because it is commented (#) out. I have added a bit of code that will prevent you from needing to type in each year from 1950-2012 but you need to complete the remainder QQQ and remove the #.


```r
#fisheries_tidy <- 
#  fisheries %>% 
#  gather(num_range('X',1950:2012), key='QQQ', value='QQQ')


fisheries_tidy <- 
  fisheries %>% 
  gather(num_range('X',1950:2012), key='year', value='catch')


tail(fisheries_tidy)
```

```
## # A tibble: 6 x 10
##   country commname spgroup spgroupname spcode sciname region unit  year 
##   <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <chr>
## 1 Zanzib~ Seerfis~      36 Tunas, bon~ 17501~ Scombe~     51 Quan~ X2012
## 2 Zanzib~ Sharks,~      38 Sharks, ra~ 199XX~ Elasmo~     51 Quan~ X2012
## 3 Zanzib~ Snapper~      33 Miscellane~ 17032~ Lutjan~     51 Quan~ X2012
## 4 Zanzib~ Spinefe~      33 Miscellane~ 17407~ Siganu~     51 Quan~ X2012
## 5 Zanzib~ Tropica~      43 Lobsters, ~ 22901~ Panuli~     51 Quan~ X2012
## 6 Zanzib~ Tuna-li~      36 Tunas, bon~ 175XX~ Scombr~     51 Quan~ X2012
## # ... with 1 more variable: catch <chr>
```

6. Use glimpse() to look at the categories of the variables. Pay particular attention to year and catch. What do you notice?

```r
glimpse(fisheries_tidy)
```

```
## Observations: 1,114,596
## Variables: 10
## $ country     <chr> "Albania", "Albania", "Albania", "Albania", "Alban...
## $ commname    <chr> "Angelsharks, sand devils nei", "Atlantic bonito",...
## $ spgroup     <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, 57, 31...
## $ spgroupname <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, billfi...
## $ spcode      <chr> "10903XXXXX", "1750100101", "17710001XX", "2280203...
## $ sciname     <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp", "Ar...
## $ region      <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37...
## $ unit        <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Quantit...
## $ year        <chr> "X1950", "X1950", "X1950", "X1950", "X1950", "X195...
## $ catch       <chr> "...", "...", "...", "...", "...", "...", "...", "...
```

_These are character type_



7. From question 6 you should see that there are a lot of entries that are missing. In R, these are referred to as NA's but they can be coded in different ways by the scientists in a given study. In order to make the data tidy, we need to deal with them. As a preview to our next lab, run the following code by removing the #. It removes the 'X' from the years and changes the catch column from a character into a numeric. This forces the blank entries to become NAs. The error "NAs introduced by coercion" indicates their replacement.


```r
fisheries_tidy <- 
  fisheries_tidy %>% 
    mutate(
      year= as.numeric(str_replace(year, 'X', '')), #remove the X from year
      catch= as.numeric(str_replace(catch, c(' F','...','-'), replacement = '')) #replace character strings with NA
    )
```

```
## Warning: NAs introduced by coercion
```


```r
head(fisheries_tidy)
```

```
## # A tibble: 6 x 10
##   country commname spgroup spgroupname spcode sciname region unit   year
##   <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <dbl>
## 1 Albania Angelsh~      38 Sharks, ra~ 10903~ Squati~     37 Quan~  1950
## 2 Albania Atlanti~      36 Tunas, bon~ 17501~ Sarda ~     37 Quan~  1950
## 3 Albania Barracu~      37 Miscellane~ 17710~ Sphyra~     37 Quan~  1950
## 4 Albania Blue an~      45 Shrimps, p~ 22802~ Ariste~     37 Quan~  1950
## 5 Albania Blue wh~      32 Cods, hake~ 14804~ Microm~     37 Quan~  1950
## 6 Albania Bluefish      37 Miscellane~ 17020~ Pomato~     37 Quan~  1950
## # ... with 1 more variable: catch <dbl>
```


8. Are the data tidy? Why?
_I think they are Tidy. Each vector has one type of data, and all data are stored in a vector. data types are appropriate, and all "empty" cells have been uniformly adressed._

9. You are a fisheries scientist studying cephalopod catch during 2008-2012. Identify the top five consumers (by country) of cephalopods (don't worry about species for now). Restrict the data frame only to our variables of interest.



```r
fisheries_tidy %>%
  select(country, sciname, spgroupname, commname, year, catch) %>%
  filter(sciname== "Cephalopoda") %>%
  filter(year >= 2008 & year<=2012) %>%
  arrange(desc(catch))
```

```
## # A tibble: 115 x 6
##    country  sciname    spgroupname               commname       year  catch
##    <chr>    <chr>      <chr>                     <chr>         <dbl>  <dbl>
##  1 Viet Nam Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2010 260000
##  2 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2012  82456
##  3 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2011  75494
##  4 China    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2012  61821
##  5 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2008  55108
##  6 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2009  54562
##  7 China    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2009  53451
##  8 China    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2010  51274
##  9 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2012  14388
## 10 India    Cephalopo~ Squids, cuttlefishes, oc~ Cephalopods ~  2010  13593
## # ... with 105 more rows
```
`

Viet Nam, India, China, Madagascar, and Cambodia

10. Let's be more specific. Who consumes the most Common cuttlefish? Store this as a new object cuttle.




```r
cuttle <- fisheries_tidy %>%
  
  select(country, sciname, spgroupname, commname, year, catch) %>%
  
  filter(year >= 2008 & year<=2012) %>%
  filter(commname == "Common cuttlefish") %>%
 
   arrange(desc(catch))

head(cuttle)
```

```
## # A tibble: 6 x 6
##   country sciname        spgroupname              commname       year catch
##   <chr>   <chr>          <chr>                    <chr>         <dbl> <dbl>
## 1 France  Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2012 13217
## 2 France  Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2011 12966
## 3 France  Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2009  8076
## 4 Tunisia Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2012  7717
## 5 Tunisia Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2011  6371
## 6 Tunisia Sepia officin~ Squids, cuttlefishes, o~ Common cuttl~  2008  4913
```

France is the highest Common cuttlefish consumer


















