---
layout: post
title: "SQL Window Functions"
tags: [SQL]
comments: true
---

##### Working with aggregate values
- Requires you to use `GROUP BY` with **all** non-aggregate columns

If you try to retrieve additional information without grouping by every single non-aggregate value, query will return an error

```sql
SELECT
    country_id,
    season,
    date,
    AGV(home_goal) AS avg_home
FROM match
GROUP BY country_id;
```

> ERROR: column "match.season" must appear in the GROUP BY clause or be used in an aggregate funtion

Thus, you can't compare aggregate values to non-aggregate data


##### Introducing window functions
- Perform calculations on an already generated result set (a window)
- Aggregate calculations
  - Similar to subqueries in `SELECT`
  - Running totals, rankings, mmoving averages
Window functions are a class of functions that perform calculations on a result set that has already been generated, also referred to as a "window"

##### What's a window function?
- How many goals were scored in each match in 2011/2012, and how did that compare to the average?

```sql
SELECT
    date,
    (home_goal + away_goal) AS goals,
    (SELECT AVG(home_goal + away_goal)
    FROM match
    WHERE season = '2011/2012') AS overall_avg
FROM match
WHERE season = '2011/2012'; 
```

The same results can be generated using the clause common to all window functions `OVER` clause. Instead if writhing a subquery, calculate the AVG of home_goal and away_goal, and follow it with the `OVER` clause. This clause tells SQL to "pass this aggregate value over this existing result set"

```sql
SELECT
    date,
    (home_goal + away_coal) AS goals,
    AVG(home_goal + away_goal) OVER() AS overall_avg
FROM match
WHERE season = '2011/2012'
```

| date       | goals | overall_goals |
|------------|-------|---------------|
| 2011-07-29 | 3     | 2.716         |
| 2011-07-30 | 2     | 2.716         |


##### Generate a RANK

```sql
SELECT
    date,
    (home_goal + away_goal) AS goals,
    RANK() OVER(ORDER BY home_goal + away_goal DESC) AS goals_rank
FROM match
WHERE season = '2011/2012'
```

| date       | goals | goals_rank |
|------------|-------|------------|
| 2011-11-06 | 10    | 1          |
| 2011-08-28 | 9     | 2          |

##### Key Differences
- Processed after every part of query except `ORDER BY`
  - Uses information in result set rather than database
- Available in PostgreSQL, Oracle, MySQL, SQL Server...
  - ...Not SQLite


