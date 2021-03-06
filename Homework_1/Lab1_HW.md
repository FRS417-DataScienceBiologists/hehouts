---
title: "Lab1_HW"
author: "Hannah Houts"
date: "January 18, 2019"
output: 
  html_document: 
    keep_md: yes
---



## Instructions:
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our GitHub repository. I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.


### 1. Navigate to the R console and calculate the following expressions.


```r
5 - 3 * 2
```

```
## [1] -1
```

```r
8 / 2 ** 2
```

```
## [1] 2
```


### 2. Did any of the results in #4 surprise you? Write two programs that calculate each expression such that the result for the first example is 4 and the second example is 16.

I was surprised that the input properly follows order of operations.
The "**" appears to be similar to "^," to exponentiate.

a)

```r
2 ** 2
```

```
## [1] 4
```

b)

```r
2**2 + 2400/200
```

```
## [1] 16
```


### 3. You have decided to use your new analytical powers in R to become a professional gambler. Here are your winnings and losses this week.


```r
blackjack <- c(140, -20, 70, -120, 240)
roulette <- c(60, 50, 120, -300, 10)
```


a. Build a new vector called days for the days of the week (Monday through Friday).

```r
days <- c("Monday", "Tuesday", "Wednesday", "Thrusday", "Friday")
```


We will use days to name the elements in the poker and roulette vectors.

```r
names(blackjack) <- days
names(roulette) <- days
```

b. Calculate how much you won or lost in blackjack over the week.

```r
total_blackjack <- sum(blackjack)
total_blackjack
```

```
## [1] 310
```

c. Calculate how much you won or lost in roulette over the week.

```r
total_roulette <- sum(roulette)
total_roulette
```

```
## [1] -60
```

d. Build a total_week vector to show how much you lost or won on each day over the week. Which days seem lucky or unlucky for you?

```r
total_week <- c(blackjack + roulette)
total_week
```

```
##    Monday   Tuesday Wednesday  Thrusday    Friday 
##       200        30       190      -420       250
```
Fridays are good, Thursdays are bad. Any day is great to reach out for a gambling problem.

e. Should you stick to blackjack or roulette? Write a program that verifies this below.

```r
Blackjack_Rules_Roulette_Drools <- total_blackjack>total_roulette
Blackjack_Rules_Roulette_Drools
```

```
## [1] TRUE
```


```r
Roulette_Rules_Backjack_Drools <- total_blackjack<total_roulette
Roulette_Rules_Backjack_Drools
```

```
## [1] FALSE
```
Blackjack is my game!


