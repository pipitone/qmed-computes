---
id: 51
title: Some thoughts on assessing understanding
date: 2017-11-02T21:07:24+00:00
author: jp
layout: post
guid: https://jon.pipitone.ca/blog/?p=51
permalink: /some-thoughts-on-assessing-understanding/
categories:
  - computing skills
  - qmed
  - teaching
---
I've been thinking about how to assess the extent to which learners are picking up the big ideas I want to teach. <a href="https://software-carpentry.org/assessment/">Software Carpentry uses self-report</a> to gauge learning. I can see this working with learners that have more of background in computing, or have specific research tasks they can use to judge their improved competence against, but for rank novices, many of whom I expect will not have the time to master the workshop skills, accurate self-assessment may be really difficult.

So, what about assessing learner's understanding of big ideas directly. Given specific tasks to solve computationally, I could look specifically for evidence of how well learners can put big ideas into play. I could grade their solutions using the following rubric:
<ul>
 	<li>None: does not know how to solve the problem</li>
 	<li>Poor: solves the problem by brute force, and does not demonstrate any competence with any big ideas, e.g. uses cut-and-paste and manual calculation</li>
 	<li>Okay: understands some of the concepts needed to solve the problem, but does not demonstrate knowing how to assemble the these into a solution, e.g. knows data tables can be read in and manipulated, but does not know specifically how</li>
 	<li>Good: demonstrates concept understanding and organized approach to solve the problem effectively, but has not mastered the specific commands and syntax, e.g. provides a recipe or pseudocode</li>
 	<li>Ideal: provides working, or near-working, instructions</li>
</ul>
Here's an example problem and different grades of solutions to illustrate what I mean:
<blockquote>Given a spreadsheet (link to example spreadsheet) with rows containing systolic (column A) and diastolic (column B) blood pressure measurements, compute the mean arterial pressure (MAP), where
<p style="text-align: center;"><tt>MAP = 1/3 * systolic BP + 2/3 * diastolic BP</tt></p>
A third column, C, contains the heart rate. If the heart rate is above 150, the mean arterial pressure is the average of systolic and diastolic blood pressure.
<ul>
 	<li>Poor: adds a column and computes by hand</li>
 	<li>Okay: "use a formula to compute MAP"</li>
 	<li>Good: "Add a column, D, and in it use a formula using cell references to compute the MAP, e.g. <tt>D = 2/3*A + 1/3*B</tt>. Use an IF function to check HR and use <tt>D = 1/2A + 1/2B</tt> instead"</li>
 	<li>Ideal: Column <tt>D = IF(C&lt;150, AVG(A, B), 2/3*A+1/3*B)</tt></li>
 	<li>Bonus points: use named ranges, create a parameter table that stores the HR=150 threshold and uses a reference to that in the formula instead of hard-coding</li>
</ul>
</blockquote>
A final section for each question could involve letting the student attempt to answer the question a second time, but this time using inline or online resources in order to assess their help-seeking competence.