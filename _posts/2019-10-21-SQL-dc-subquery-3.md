---
layout: post
title: "Intermediate SQL Subquerys in SELECT"
tags: [Datacamp, SQL]
comments: true
---

##### SELECTing what?
- Returns a single value
  - Include aggregate values to compare to individaul valuse
  - Used in mathematical calculations
    - Deviation from the average

##### Subqueries in SELECT
- Calculate the total matches


##### practice 1: Add a subquery to the SELECT clause

Subqueries in `SELECT` statements generate a single value that allow you to pass an aggregate value down a dataframe. This is useful for performing calculations on data within your database.

In the following excercise, you will construct a query that calculates the average number of goals per match in each country's league

```sql
SELECT 
	l.name AS league,
    -- Select and round the league's total goals
    ROUND(AVG(m.home_goal + m.away_goal),2) AS avg_goals,
    -- Select and round the average total goals
    (SELECT ROUND(AVG(home_goal + away_goal),2) 
     FROM match
     WHERE season = '2013/2014') AS overall_avg
FROM league AS l
LEFT JOIN match AS m
ON l.country_id = m.country_id
-- Filter for the 2013/2014 season
WHERE m.season = '2013/2014'
GROUP BY l.name;
```
