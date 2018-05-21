---
title: Visualisation in R Post-mortem
date: 2018-03-28
layout: post
---

I ran this workshop more interactively than others: with me jockeying at the
R console, writing bits of code to introduce ggplot concepts, and asking the
group questions as I went, and getting them to offer suggestions and guess as to
the outcome of commands as we organically worked towards preparing a plot with a
single dplyr/ggplot pipeline. 

My plan going in was:

1. Review the core `dlyr` verbs: `filter()`, `mutate()`, `group_by()`,
   `summarize()`
2. Explain the basic structure of a ggplot command: `ggplot(aes())` + layer +
   layer + ...
3. Demonstrate more "advanced" features of ggplot, like facetting, which
   required rearranging our dataset with `gather` and `spread`. 

Here are my take-aways from this session: 

- People enjoyed this session. I think it was a combination of the change of pace,
  and general exhaustion at this point in the year meant it was nice to sit back
  and participate but not have to bang your head against the wall trying to
  learn something from scratch. 
- I spent far longer reviewing `dplyr` than I expected. It had been about a
  month since our session on [Data Wrangling
  workshop](https://pipitone.github.io/qmed-computes/data-wrangling.html) and I
  think most people had forgotten just about everything. 
- Introducing a ggplot command veeerrrrry slowly by building it up from parts
  was effective. I started with just `data %>% ggplot()`, introduced aesthetics
  and got everyone to appearance of axes, and then introduced different geoms
  and other layers and styling commands. 
- `gather` and `spread` are mysterious and seem like magic... I don't think
  people came away from this session feeling like they understood the syntax,
  but I do think they have some understanding of what these commands do and why
  they are necessary for ggplot. Maybe. I'll make sure to demonstrate these
  commands again in other lessons. 
- At the 1.5 hour mark, people were toast. No one went on to do the DataCamp, or
  Carpentry lessons. I think people are just tired. 

In short: the interactive call-and-response lesson format was well-received, but
I'm not sure how much in the way of concrete skills people have left with. 
