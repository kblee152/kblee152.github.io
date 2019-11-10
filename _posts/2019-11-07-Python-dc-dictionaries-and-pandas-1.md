---
layout: post
title: "Intermediate Python: Dictionaries & Pandas (1)"
tags: [Datacamp]
comments: true
---

#### List
Use below index to subset the pop list, to get the population corresponding to Albania  
We built two lists, and used the index to connect corresponding elements in both lists.
(It worked, but it's a pretty terrible approach: it's not convenient and not intuitive)


```python
pop = [30.55, 2.77, 39.21]
countries = ["afghanistan", "albania", "algeria"]

ind_alb = countries.index("albania")
ind_alb # print out 1

pop[ind_alb] # print out 2.77
```
