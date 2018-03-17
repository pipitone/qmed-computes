---
layout: page
title: Spreadsheets
subtitle: Using spreadsheets effectively
icon: fa-th
order: 3
---

Workshop date: 2017-11-17   
Author: Jon Pipitone, 2017

## Big ideas
Here are the big takeaways I'd like you to leave with: 

1. <span class="big-idea">Plan for machines to read your data.</span>  
   Keep your data retangular. Be
   consistent with naming and values. Don't use colors to indicate anything
   meanful.

1. <span class="big-idea">Be able to explain your work.</span>  
   Decide what is raw data, and never edit it.
   Add new columns to clean it up or derive new values. 

1. <span class="big-idea">Make the computer compute.</span>  
   Don't do anything by hand that you can
   automate. This shows your work, and lets you fix problems later easily.


## Learning objectives
- Absolute/relative references in formulas
- Know how formulas update, and what happens to cell references when copied/fill
- Know how to use parameter tables to factor out constants in formulas
- Use V/HLOOKUP() to fill in data or merge tables
- Use IF() to create indicator columns or conditional formulas
- Know that other formulas exist: e.g. AVG, AVGIF, SUM, SUMIF, and COUNTIF()
- Know that date/text/number columns are displays only, and how to change these
- Know best practices for organizing tabular data
	- use tabular format: 
		- columns as features, rows as observations, 
		- column names in first row
		- column names with no spaces or special characters
		- ID column with absolute unique ID
	- consistency when entering “factor” columns (e.g. use “Y” or “N”, not “Y”, “Yes”, “yes”, etc..)
	- avoid colors for anything meaningful
	- never edit raw data, instead make derived columns
- Know how to navigate the inline and online help (e.g. stackoverflow) for problem-solving


## Tasks

### Part 1 - The very basics
For the following tasks, you will be creating and then working with some dummy
study data.

My solution to these tasks, and some extra data you'll need along the way can be
found in the
[spreadsheets-solutions.xlsx](assets/workshop-data/spreadsheets-solution.xlsx)
spreadsheet.

Note: Throughout all of this, consult the inline help, as well as online
resources (hint: [stackoverflow.com](https://stackoverflow.com)).

1. Create some dummy vitals data for some fictional study participants with the following columns: 

    - `participant_id`: this should be a unique number, and start with a the
      study code 'ST001' and separated by a '_', e.g. `ST001_12`, `ST001_47`
    - `age`: participant age
    - `HR`: a plausible heart rate, from 50-220 
    - `RR`: a plausible respiratory rate, e.g. 5-40
    - `diastolic`: a plausible but random blood pressure
    - `systolic`: a plausible but random blood pressure

    Create records for 100 participants. 

    **Hint: Use a formula to generate randomly numbers**

    What happens when you copy-and-paste a formula from one column to another? 

    Why does the data keep changing? When does it change? 

1. To stop the fabricated data from constantly changing, create a new sheet, and
   paste just the *values* into it. 

    Hint: Select, copy, and choose "Paste special.." > "Paste as values"

1. Add a new column to compute their Mean Arterial Pressure (MAP): 
   
        MAP = 1/3 systolic + 2/3 diastolic

1. Adjust the formula so that MAP is properly calculated for high heart rates,
   i.e 
   
        If HR > 100, MAP = 1/2 systolic + 1/2 diastolic
        otherwise, MAP = 1/3 systolic + 2/3 diastolic

1. (Optional) Format the MAP column to display results rounded to the nearest integer
   
   How would you do this with a formula? When should you? 

1. Factor out the 100 from the above formula into a parameter table on a new tab

   Hint: you will need to use absolute cell references  
   Optional: You can also factor out the Study ID name "ST001" as well  
   Optional: Try using a named range rather than an absolute cell reference

1. Compute the average MAP, average MAP for high HR (>100) subjects, and average
   MAP for normal HR subjects. Put these on the Parametres and Summary sheet so
   that they don't clutter the data tables. 

   Hint: Use AVERAGEIF()

   Bonus (if you have time): Use the MAP HR Threshold value you factored out in
   your AVERAGEIF() command so that if you change the threshold, your averages
   change too.

   Hint (for the bonus): You'll want to create a string showing the condition to
   be met, but substitute the threshold value in. To do this, use the `&`
   operator (or `CONCAT()`). Isn't that gross? 


### Part 2 - Merging
There is some additional data for each participant on the Investigations sheet
in the google doc linked above that you now need to merge into your data table.
Unfortunately, not all of the subjects have this extra data.  C'est la vie. 

1. Copy the Investigations data into a new sheet in your workbook. 

1. Merge the `confusion` column. Create a new column in your data table named
   'confusion', and make use of the VLOOKUP() function to grab the appropriate
   value from the Investigations sheet based on the `participant_id`. 

   Hint: this is tricky.

   What are the `#N/A` values that show up? Should they be there? What if you
   wanted a different value instead of `#N/A`? 

1. Merge the `urea` column. 

1. Optional: Clean up the `confusion` column, since as it stands it will be
   *confusing* to work with. Create a new column, `confusion_tidy` that is
   either 'Yes", or "No" (or use the built in True/False). 

   Hint: A glamorous way to do this by using SWITCH(). 

1. Optional: compute the CURB-65 score, where a participant gets a point for
   each of the following conditions: 

    - They have confusion (ignore this if you haven't cleaned up the `confusion`
      column)
    - Urea > 7
    - RR > 30
    - systolic < 90 or diastolic < 60
    - Age > 65

   Hint: Create a new column for each of these conditions and calculate the
   score, e.g. `CURB65_confusion`, etc. Then create a final column and sum up
   the individual scores

   Why should you do it this way rather than creating a single formula? 

### Part 3 - Tidy data

Work through the [Data Carpentry spreadsheet lesson](http://www.datacarpentry.org/spreadsheet-ecology-lesson/).

This lesson includes all the big ideas you should take away from this workshop.
Be sure to have a glance through the [Instructor
notes](http://www.datacarpentry.org/spreadsheet-ecology-lesson/guide/) also. 

Note: these lessons are designed around Excel, and you may need to modify them
if you are using OpenOffice Calc, or Google Sheets.

## Other resources 

- [Use of Spreadsheets for Research Data Collection and Preparation: A Primer](https://www.ncbi.nlm.nih.gov/pubmed/26454810)

   This paper that summarizes all the important points about how to structure
   your spreadsheets and record data in a uniform way. 

- [Good enough practices in scientific computing](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5480810/)

   You may not think you are doing "scientific computing" but welcome to the
   21st century: you probably are. This paper outlines the basic strategies you
   should strive towards when you get going. 
