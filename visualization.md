---
layout: page
title: Visualization
subtitle: 
icon: fa-bar-chart
order: 7
---

Workshop date: 2018-04-28  
Author: Jon Pipitone, 2018

This workshop is an interactive exploration of `ggplot`, the plotting library
that is part of the `tidyverse`.

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

Script
------

Since this workshop was interactive, there was no set of specific tasks to
follow. Here's a script from one of the sessions that covers some of what we
did: 


```r

install.packages('tidyverse')
library(tidyverse)

download.file(
  url = 'https://pipitone.github.io/qmed-computes/assets/workshop-data/ggplot-timeseries.csv',
  destfile = 'data.csv')

# Review some data wrangling

data = read_csv('data.csv')

spo2_table = data %>% 
  select(Time, SpO2)

spo2_table = data %>% 
  select(-Time)

data2 = data %>% 
  select(Time, HR, SpO2) %>%
  filter(HR < 100) %>%
  mutate(tachy = HR > 100, 
         test = SpO2 / 100)

write_csv(data2, 'data2.csv')

# make a simple scatter/line plot
data %>%
  filter(HR < 120) %>%
  ggplot(aes(x = Time, y = HR)) +
    geom_line() + 
    geom_point() +
    labs(
      title = "Title", 
      subtitle = "subtitle", 
      x = "Time (s)",
      caption = "Source: David Wood"
    ) + 
    theme_minimal()

# use gather() to rejig our data to make it possible to plot by measurement
data %>%
  mutate(tachy = HR > 100) %>%
  gather(Measurement, Value, -Time, -tachy) %>%
  ggplot(aes(x = Time, y = Value, colour = Measurement)) + 
    geom_point() + 
    geom_line() + 
    facet_wrap(~ Measurement)

```

Resources 
---------

- [tidyverse documentation](https://www.tidyverse.org/packages/). This is the
  source for the `dplyr` and `ggplot2` libraries, and good starting place to
  learning how to use them and related libraries. In particular, check out [R
  for Data Science](http://r4ds.had.co.nz/): a book for written by the author of
  the tidyverse. 

- [Data Carpentry's lesson on Data vis with
  ggplot2](http://www.datacarpentry.org/R-ecology-lesson/04-visualization-ggplot2.html)

- [DataCamp's Data visualization with ggplot2
  course, Part 1](https://www.datacamp.com/courses/data-visualization-with-ggplot2-1)
  There is a [part 2](https://www.datacamp.com/courses/data-visualization-with-ggplot2-2)
