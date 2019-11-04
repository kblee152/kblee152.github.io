---
layout: post
title: "Intermediate SQL Window Functions OVER AND PARTITION BY"
tags: [Datacamp, SQL]
comments: true
---

##### OVER and PARTITION BY
- Calculate separate values for different categories
- Calculate different calculations in the same column

```sql
AVG(home_goal) OVER(PARTITION BY season)
```

This will then return the overall average for, or `PARTITION BY` each season


##### Partition your data
- How many goals were scored in each match, and how did that compare to the overall average?

```sql
SELECT 
    date,
    (home_goal + away_goal) AS goals,
    AVG(home_goal + away_goal) OVER() AS oversall_avg
FROM match;
```

| date       | goals | overall_avg |
|------------|-------|-------------|
| 2011-12-17 | 3     | 2.73        |
| 2012-05-01 | 2     | 2.73        |

- How many goals were scored in each match, and how did that compare to the season's average?

```sql
SELECT
    date,
    (home_goal + away_goal) AS goals,
    AVG(home_goal + away_goal) OVER(PARTITION BY season) AS season_avg
FROM match;
```

| date       | goals | season_avg |
|------------|-------|------------|
| 2011-12-17 | 3     | 2.71       |
| 2012-05-01 | 2     | 2.71       |
| 2012-11-27 | 4     | 2.77       |

##### PARTITION by Multiple Columns

```sql
SELECT
    c.name,
    m.season,
    (home_goal + away_goal) AS goals,
    AVG(home_goal + away_goal)
        OVER(PARTITION BY m.season, c.name) AS season_ctry_avg
FROM country AS c
LEFT JOIN match AS m
ON c.id = m.country_id
```
The result set returns the average goals scored broken out by season and country

| name        | season    | goals | season_ctry_avg |
|-------------|-----------|-------|-----------------|
| Belgium     | 2011/2012 | 1     | 2.88            |
| Netherlands | 2014/2015 | 1     | 3.08            |

##### PARTITION BY considerations
- Can partition data by 1 or more columns
- Can partition aggregate calculations, ranks, etc