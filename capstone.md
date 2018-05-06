---
layout: page
title: Capstone Project
subtitle: 
icon: fa-star
order: 9
---

In this session you will work in pairs to explore a dataset using the skills
you've learned in this series. 


Workshop date: 2018-05-06 

Author: Jon Pipitone, 2018


Learning objectives
-------------------
- Practice using your skills of: 
    - Data organization and formulas in spreadsheets
    - Cleaning up messy data and exploring using OpenRefine
    - Data Wrangling and Visualisation in R

Tasks
-----
In this session we'll use a dataset of expenses from Yannay: [Expenses-Budget2.xlsx](https://pipitone.github.io/qmed-computes/assets/workshop-data/Expenses-Budget2.xlsx)

1. Download it the data (perhaps using `download.file()`?)

2. Get a feel for the data by opening it as a spreadsheet or using OpenRefine

3. Come up with a few specific questions you have of the data, and decide how
   you will go about answering them using Spreadsheets/OpenRefine/R

## Consider the following
- Do you need edit the spreadsheet at all before you use it in OpenRefine? Why?
  That is, does this spreadsheet follow the best practices we discussed? 
- How do you know whether an entry is an expense or income? 
- Look at the columns for specifying the date... Will you need to make any
  changes? (ps. dates are complex. The `lubridate` package is great for managing
  dates in R)

## Some questions to get you started 
- How much does Yannay spend per month?
- Has that changed over the years? 
- What does he spend the most on every month beside tuition and rent? 
- How well can you predict his monthly spending on eating out based on
  everything else you know? 

