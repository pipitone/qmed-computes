---
layout: page
title: Data Wrangling
subtitle: Using R and the dplyr package to get your data in order
icon: fa-crop
order: 6
---

Workshop date: 2018-02-23  
Author: Jon Pipitone, 2018

Big Ideas
---------

Here are the big takeaways I’d like you to leave with from this
workshop:

- <span class="big-idea">Automate. Don't manipulate data by hand.</span> `dplyr`
  gives you functions ("verbs") to express how to manipulate your data in code.
  This is repeatable, and precise. 

- <span class="big-idea">Pipes: functions that transform data</span>. Seeing
  functions a machines that take input, transform, and produce output is an
  important paradigm in computing that will come up again and again.

Learning objectives
-------------------

- Review RStudio, and parts of the IDE: console, editor, heap
- Review R variables and calling functions
- Install and load libraries using `install.packages()`, `library()`
- Learn about [`tidyverse`](https://www.tidyverse.org/), and what `dplyr` is for
- Load data using `read_csv()`
- Add columns to a tibble using `mutate()`
- Extract columns using `select()`
- Write "pipelines" using the `%>%` operator
- Subset rows using `filter()`
- Aggregate a dataset using `summarise()`
- Aggregate by groups using `group_by()`
- Merge tables using `inner_join()` and friends

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
1. Install the `hflights` package and load it

In this workshop, we will be redoing some of the analysis we did in the
[spreadsheets](spreadsheets.html) workshop. You can download CSV versions of
the sheets here:
- [vitals.csv](assets/workshop-data/data-wrangling/vitals.csv)
- [investigations.csv](assets/workshop-data/data-wrangling/investigations.csv)

You can also download this data directly from R using the following code: 

```r
download.file("https://pipitone.github.io/qmed-computes/assets/workshop-data/data-wrangling/vitals.csv",
    destfile="vitals.csv")
download.file("https://pipitone.github.io/qmed-computes/assets/workshop-data/data-wrangling/investigations.csv",
    destfile="investigations.csv")
```

In this workshop, we will follow the [DataCamp lesson on `dplyr`](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial).

### Introduction to dplyr and the tidyverse

1. Review some relevant R 
    - `a = 1` means the variable `a` gets the value `1`
    - Variable assignment may also be written `a = 1`
    - Functions look like they do in excel, e.g. `max(4,6,20,1)`
    - You can assign the results of a function to a variable, e.g. `a = max(4,6,20,1)`
    - Get help on any function by using the `help()` function, e.g. `help(max)`
    - There are several useful functions for exploring data tables. Have a look
       at the `hflights` data: 

   ```r
library(hflights)
library(tidyverse)
colnames(hflights) 
nrows(hflights)
head(hflights)
```

1. Watch the [DataCamp video describing the `hflights`
   data](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-one-introduction-to-dplyr-and-tbls?ex=4)

1. Watch the [intro to dplyr commands, called
   "verbs"](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-two-select-and-mutate?ex=1)

Questions? 

### Selecting columns

1. Do the DataCamp [exercise on using `select`](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-two-select-and-mutate?ex=3)

1. Load the vitals.csv data using the `read_csv()` function
    ```r
    vitals_csv = read_csv('vitals.csv')
    # read_csv will spit out information about how it guessed the column formats
    ```

1. Take a look at the columns (hint: `colnames()`), and the data itself
   (`head()`)

1. Use `select()` to extract the columns starting with `participant_id` through
   to `diastolic` into a new variable `vitals`:
   ```r
   vitals = select(vitals_csv, participant_id, age, sex, HR, 
                   oxygen_sat, RR, temp, systolic, diastolic)
  
   # here's a shortcut
   vitals = select(vitals_csv, participant_id:diastolic)
   ```
1. Explore the table stored in `vitals` and `vitals_csv` by just typing the
   variable names out on the console to display them, and also by using
   `head()`, `colnames()`, or the RStudio IDE

### Adding columns

1. Watch the [DataCamp video on `mutate()`](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-two-select-and-mutate?ex=6). 

1. Do the two exercises that follow the video only.

1. Use `mutate()` to add a `MAP` column computed using the following formula,
   and store the resulting data table in a new variable called `vitals_MAP`: 

        MAP = 1/3 systolic + 2/3 diastolic

1. Bonus: use the function `ifelse()` to set the mean arterial pressure based on
   heart rate: 

        If HR > 100, MAP = 1/2 systolic + 1/2 diastolic
        otherwise, MAP = 1/3 systolic + 2/3 diastolic

    hint: your call to mutate will look something like: `mutate(vitals, MAP = ifelse(...))`

### Filtering data

1. Watch the [DataCamp video on `filter()`](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-three-filter-and-arrange?ex=1) and do the three exercises that follow (everything up to `arrange()`). 

1. Practice using `filter()` to grab parts of the vitals dataset, e.g: 
    1. Find all subjects older than 65
    1. Find all febrile subjects
    1. Find all subjects that are tachycardic but afebrile
    1. Find all subjects with any concerning vital

### Arrange

`arrange()` sorts your data tables. It can be useful, but I recommend learning
about this some other time. 

### Summarizing a dataset

1. Watch the [DataCamp video on
   summarise()](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-four-summarise-and-the-pipe-operator?ex=1)

1. Do the exercise the follows the video. You can do the other exercises, but
   they require you to know about NA values and how to filter them using the
   `is.na()` function, which we haven't covered.

### Syntactic suger: Pipes

1. Watch the [DataCamp video on chaining
   functions](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-four-summarise-and-the-pipe-operator?ex=5).
   Fair warning: this video might be a tad confusing at first. 

2. Skip the exercise that immediate follows the video, and do the two "Drive or
   fly" exercises instead.

3. Write your code that selects, mutates, and filters the vitals data from the
   previous exercises using pipes. My answer is below. 

### Summarising by groups

1. Watch the [DataCamp video on
   `group_by`](https://campus.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/chapter-five-group_by-and-working-with-databases?ex=1)

2. Do the exercise that follows. 

3. Now, let's figure out the average age for participants who are tachycardic,
   and those who aren't.  First, group by the vitals dataset by HR > 100, then
   summarise by computing the `avg_age` as the mean age. 

   My answer is below. 


### Merging tables

1. Load up the investigations.csv data, and explore it to remind yourself of the
   columns and the data. Note that we don't have investigations for all of the
   subjects. 

2. Also, note that the vitals table and the investigations tables share the
   `participant_id` column. If we wanted to merge the tables, we have to use
   this column to match rows. We can do this with a "join" function. There are
   several flavours depending on how exactly you want to do the merge. Run
   `help(join)` to find out more. 

3. If we want to merge all of the investigations data into the vitals table, and
   include empty values when the investigations are missing, we can use the
   `left_join` function: 

   ```r
   vitals = read_csv('vitals.csv')
   investigations = read_csv('investigations.csv')
   merged = left_join(vitals, investigations, by = 'participant_id')
   ```
4. What does `right_join` do differently?

5. What does `inner_join` do? 


### Putting it all together 

Compute the average MAP for participants with uremia (urea > 7) by sex. 

-------


Answers
-------

### Pipes

```r
read_csv('vitals.csv') %>%
   select(participant_id:diastolic) %>%
   mutate(MAP = 1/3 * systolic + 2/3 * diastolic) %>%
   filter(temp > 38.0) 
```

### Summarising by groups

```r
vitals %>% 
    group_by(HR > 100) %>%
    summarise(avg_age = mean(age))
```

### Putting it all together

```r
investigations = read_csv('investigations.csv')

read_csv('vitals.csv') %>%
    select(participant_id:diastolic) %>%          # this isn't really necessary
    filter(urea > 7) %>%
    mutate(MAP = 1/3 * systolic + 2/3 * diastolic) %>%
    left_join(investigations) %>%                 # tables joined on participant_id automatically!
    group_by(sex) %>%
    summarise(avg_MAP = mean(MAP))
```

Resources
---------

- DataCamp's [Introduction to the
  tidyverse](https://www.datacamp.com/courses/introduction-to-the-tidyverse?tap_a=5644-dce66f&tap_s=213362-c9f98c)
  course.

  The first chapter goes through the important parts of the `dplyr` verbs with
  a different dataset.

- Data Carpentry's lesson on [Manipulating and analysing data with
  dplyr](http://www.datacarpentry.org/R-ecology-lesson/03-dplyr.html).
  
  This is another great walkthrough of dplyr that includes some other more
  interesting features. 

- [R for Data Science](http://r4ds.had.co.nz/)

  This online book is a great and practical, analysis-focused resource for
  learning dplyr and the rest of tidyverse, written by the person who
  spearheaded the tidyverse itself. 

- [tidyverse.org](https://www.tidyverse.org/learn). The website for the
  tidyverse project has lots of good links out to resources to learn. 

