---
layout: page
title: Visualization
subtitle: 
icon: fa-bar-chart
order: 7
---

Workshop date: 2018-04-28  
Author: Jon Pipitone, 2018

Big Ideas
---------

Here are the big takeaways I’d like you to leave with from this
workshop:

- <span class="big-idea">Restructure your data to make plotting easier</span>
  
  For certain kinds of visualizations, it helps to first reorganize your data.
  For instance, rather than columns for each kind of measurement, we use a new
  row.
  ```
  Time    Measurement   Value
  11:11   HR            65 
  11:11   SpO2          99
  11:12   HR            110
  11:12   SpO2          87
  ...
  ```
- <span class="big-idea">Pipe/filter your data to ggplot</span>

  You can pipe your data directly to `ggplot` but massage it along the way using
  `dplyr` verbs to get just want you want to plot. 
  
- <span class="big-idea">Create charts by adding layers</span>

  With `ggplot`, you add layers or override default attributes of your plot to
  specify what should be present. 

Learning objectives
-------------------
- Review RStudio, and parts of the IDE: console, editor, heap
- Install and load libraries using `install.packages()`, `library()`
- Review the "pipe and filter" model of `dplyr`
- Review `dplyr` verbs: select, mutate, filter
- Introduce piping tibbles to `ggplot()`
- Use "aesthetics", `aes()`, to specify which data attributes to use in a plot
- Create different visualizations of the data with `geom_point`, `geom_line`,
  `geom_bar`, `geom_histogram`, `geom_boxplot`
- Use `dplyr`'s `gather` function to "tidy" your dataset
- Create arrays of plots using `facet_wrap`
- Customizing labels and other accessories on plots
- Exporting/saving plots using `ggsave()`

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
1. Download the dataset: 
    ```r
    download.file(
        'https://pipitone.github.io/qmed-computes/assets/workshop-data/ggplot-timeseries.csv',
        destfile = 'data.csv')
    ```
