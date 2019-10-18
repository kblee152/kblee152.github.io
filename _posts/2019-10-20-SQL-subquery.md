---
layout: post
title: "SQL Subquery"
tags: [SQL]
comments: true
---

##### What is a subquery?
- A query nested inside another query

```sql
SELECT column
FROM (SELECT column
      FROM table) AS subquery;
```
- Useful for intermediary transformations

##### What do you do with subqueries?
- Can be in any part of a query(to use for filtering or joining)
  - `SELECT`, `FROM`, `WHERE`, `GROUP BY`
- Can return a variety of information
  - Scalar queantities (`3.14159`, `-2`, `0.001`)
  - A list(`id = (12, 25, 392, 401, 939)`)
  - A table

##### Why subqueries?
- Comparing groups to summarized values
  - How did Liverpool compare to the English Premier League's average performance for that year?
- Reshaping data
  - What is the highest monthly average of goals scored in the Bundesliga?
- Combining data that cannot be joined
  - How do you get both the home and away team names into a table of match results?