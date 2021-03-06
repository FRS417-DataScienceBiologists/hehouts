---
title: "Midterm_Completed"
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

## Instructions
This exam is designed to show me what you have learned and where there are problems. You may use your notes and anything from the `class_files` folder, but please no internet searches. You have 35 minutes to complete as many of these exercises as possible on your own, and 10 minutes to work with a partner.  

At the end of the exam, upload the complete .Rmd file to your GitHub repository.  

1. (1 point) Load the tidyverse.

2. (2 points) For these questions, we will use data about California colleges. Load the `ca_college_data.csv` as a new object called `colleges`.

3. (1 point) Use your preferred function to have a look at the data and get an idea of its structure.

4. (1 point) What are the column names?

5. (3 points) Are there any NA's in the data? If so, how many are present and in which variables?

6. (3 points) Which cities in California have the highest number of colleges?

7. (4 points) The column `COSTT4_A` is the annual cost of each institution. Which city has the highest cost?

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
