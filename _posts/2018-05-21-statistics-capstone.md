---
title: Statistics and Capstone Project
date: 2018-05-21
layout: post
---

This was the last session of the series. The plan with this session was to make this a two parter: 

- Part 1 (~30 minutes): a [brief and whirlwind tour of linear
  modelling](https://pipitone.github.io/qmed-computes/statistics.html) using
  `lm()` as a way to introduce R's syntax for formulae and hint at the
  usefulness of R's base stats package

- Part 2 (~1.5 hours): a [Capstone
  project](https://pipitone.github.io/qmed-computes/capstone.html) using where
  learners were given some raw data and told to go wild analyzing it using the
  skills we've covered in the series so far. The dataset was a fun one: one of
  the students, Yannay, has tracked two years of his finances down to individual
  purchases. 

It ended up that we held a co-working session a week after the formal session
which some people came to so as to keep working on the Capstone project, so
learners got an additional 2 hours to work on the project. 

Overall, I have mixed feelings about this session: I tried to do too much in one
sitting, and the learners probably weren't far enough along to jump into a
project like this on their own, but on the whole people seemed to enjoy the
chance to play with an interesting dataset and practice their skills. 

My take-aways: 
- I didn't teach statistics, I just taught *how* to run linear models in R, some
  of the learners were completely lost in Part 1. If I were to do this again,
  I'd have an longer session devoted to linear modelling... maybe even two.
- Because I tried crammed linear modelling into 30 minutes, it was entirely a
  show-and-tell style session. This meant that even if people had enough of a
  background in statistics to follow along, they didn't get any time to
  practice. I was hoping those people who were keen to practice their stats
  would use the Capstone project time to do that, but I think they spent most of
  the time working on the data wrangling and visualization tasks.
- As much as I wanted learners to dive into the data, and go back to earlier
  lessons to recall various clean up and data wrangling and visualization
  techniques to apply them, most weren't able to. It was just too much of a
  stretch to, say, ask of learners to remember the concept and syntax to
  `filter()` data from two lessons back. Worse, when it came to some of the more
  abstract concepts like `group_by` and `summarise` -- which I think people
  started to understand during the lesson -- learners were totally out of their
  depth without some nudging. 
- As a result, in the first session, I ended up walking people through how to
  plot the amount of money spent each month. I think learners found that useful
  and used that code to answer other related questions (mean spending per month,
  spending per year, spending across categories, etc.). Note to self: always
  give people starter code. 
- Dates are hard. I hadn't taught anything about date manipulation, and the
  dataset we used had numeric Year, Month, and Day columns. I ended up just
  gesturing at the magic of the `ISOdate()` function and letting learners know
  about the `lubridate` package if they wanted to dive into date handling
  more fully. 
- The co-working session was great. Only a few people attended, but I think they
  made good use of the extra time to play around with the dataset, and we had
  some good interactive discussions about dplyr, and ggplot. I think if I ran
  these types of co-working sessions once a month, along with lessons, everyone
  would have practiced a whole lot more. 
