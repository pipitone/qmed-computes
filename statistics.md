---
layout: page
title: Mini-session on Statistics 
subtitle: 
icon: fa-plane
order: 8
---

Workshop date: 2018-05-06 

Author: Jon Pipitone, 2018

Big Ideas
---------

This a short session to make room for you work on the exploratory data analysis
project, so there's only one big take away from this session: 

- <span class="big-idea">Use a formula to specify a statistical model</span>
 
  `response ~ predictors`

  Formulas are R's way of describing statistic models. The LHS is the response
  variable, and the RHS is expresses how to model the predictors for the
  response. 


Learning objectives
-------------------
- Introduce specifying models using formulas (`response ~ predictors`)
- Model data using a linear model with `lm()`
- Model an interaction with `lm()`
- Demonstrate using `predict()`, and the `modelr` package to predict values
  with a model
- Inspect a model with `summary()`
- Using formulas in other parts of R, e.g. `t.test()`, `facet_wrap()`

Tasks
-----

### Set up 
1. Install RStudio and R
1. Install the `tidyverse` package using the `install.packages` function, and load it using
   the `library()` function: 
   ```r
   install.packages('tidyverse')     # this may take some time
   library(tidyverse)
   ```
1. Load the `modelr` package: `library(modelr)`


### Script

In this session I'll be demoing R's statistical features, mostly borrowing from  
the excellent [R for Data Science](http://r4ds.had.co.nz/) book's chapter on
[Modelling](http://r4ds.had.co.nz/model-intro.html)


This is the script I will follow: 

```r
# take a look at the sim1 dataset. It's just x and y values
sim1 

sim1 %>% ggplot(aes(x=x,y=y)) + 
  geom_point()

# make a linear model of the y values from the x values
sim1.lm = lm(y ~ x, data=sim1)

# y ~ x is a  formula
# 
# When a formula is used by lm it is interpreted as a linear model
# equivalent to the polynomial: 
#   y = a0 + a1*x
#
# where a0 and a1 are coeffients of the fitted line

sim1.lm
sim1.lm$coefficients
sim1_lm_intercept = sim1.lm$coefficients[1]
sim1_lm_slope =  sim1.lm$coefficients[2]

# we can plot this line to see it's fit
sim1 %>% ggplot(aes(x=x,y=y)) + 
  geom_point() + 
  geom_abline(intercept = sim1_lm_intercept, 
              slope = sim1_lm_slope)

# in fact, this line is exactly what geom_smooth produces
sim1 %>% ggplot(aes(x=x,y=y)) + 
  geom_point() + 
  geom_smooth(method="lm")  

# the model, stored in sim1.lm, can be explored directly: 

summary(sim1.lm)
plot(sim1.lm)
anova(sim1.lm)



# We can also use the model to make predictions
predict(sim1.lm, data.frame(x = sim1$x))

# The modelr package has functions for computing the predictions and attaching
them to the dataset in a new column
sim1 %>% 
  add_predictions(sim1.lm)




# Formulas can specify many predictor terms, and how to combine them

# First, consider this new dataset with a categorical predictor, x2
sim3
sim3 %>% 
  ggplot(aes(x=x1, y=y, colour=x2)) + 
    geom_point()

# We can model x2 as an interaction term or not
no_interaction = lm(y ~ x1 + x2, data = sim3)
interaction = lm(y ~ x1 * x2, data = sim3)

# some modelr magic to produce predictions for both models
grid <- sim3 %>% 
  data_grid(x1, x2) %>% 
  gather_predictions(no_interaction, interaction)
grid

# ... and now plot predictions as lines to visualise them
ggplot(sim3, aes(x1, y, colour = x2)) + 
  geom_point() + 
  geom_line(data = grid, aes(y = pred)) + 
  facet_wrap(~ model)

# the interaction model is exactly what geom_smooth() produces
sim3 %>% 
  ggplot(aes(x=x1, y=y, colour=x2)) + 
  geom_point() + 
  geom_smooth(method="lm")




# Formulas are used throughout R
# Here's an example of using a formula to compute a T-test 

# Sleep dataset with two groups
sleep
sleep %>% 
  ggplot(aes(x=extra, fill=group)) + 
    geom_histogram()

# the nasty way of comparing both groups
t.test(sleep$extra[sleep$group == 1], sleep$extra[sleep$group == 2])

# slightly better, using our dplyr know-how
group_1 = sleep %>%
  filter(group == 1)
group_2 = sleep %>%
  filter(group == 2)
 
t.test(group_1$extra, group_2$extra)

# using a formula
t.test(extra ~ group, data = sleep)

# check the help for t.test to understand how the formula is interpreted
```


Resources 
---------

- The [R for Data Science](http://r4ds.had.co.nz/) is a good introduction to
  modelr, and statistical modelling in general. It balances teaching you about
  statistical modelling, and showing off the tidyverse way of doing it.

- [DataCamp's Intro to Statistics with R](https://www.datacamp.com/tracks/learn-statistics-with-r)
  This course assumes you know very little about statistical methods, and walks
  you through it. Recommended if you have no background in stats, like me.  :-)
