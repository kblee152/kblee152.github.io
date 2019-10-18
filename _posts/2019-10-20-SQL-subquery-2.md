---
layout: post
title: "SQL Subquerys in FROM"
tags: [SQL]
comments: true
---

subqueries in `WHERE` can only return a single column. if you want to return a more complex set of results, subquery in the `FROM` statement are a robust tool for restructuring and transforming your data.

##### Subqueries in FROM
- Restructure and tranform your data
  - Transforming data from long to wide before selecting
  - Prefiltering data
- Calculating aggregates of aggregates
  - Which 3 teams has the highest average of home goals scored?
    - Calculate the `AVG` for each team
    - Get the 3 highest of the `AVG` values

##### FROM subqueries...

```sql
SELECT
    t.team_long_name AS team,
    AVG(m.home_goal) AS home_avg
FROM match AS m
LEFT JOIN team AS t
ON m.hometeam_id = t.team_api_id
WHERE season = '2011/2012'
GROUP BY team;
```

| team           | home_avg |
|----------------|----------|
| 1. FC Koln     | 1.1372   |
| 1. FC Nurnberh | 1.27     |

##### ...to main queries

```sql
FROM (SELECT
        t.team_long_name AS team
        AVG(m.home_goal) AS home_avg
      FROM match AS m
      LEFT JOIN team as t
      ON m.hometeam_id = t.team_api_id
      WHERE season = '2011/2012'
      GROUP BY team) AS subquery
```
make sure to give it an alias `subquery`  
then add it to the main query, selecting the team, and home_avg columns

```sql
SELECT team, home_avg
FROM (SELECT
        t.team_long_name AS team
        AVG(m.home_goal) AS home_avg
      FROM match AS m
      LEFT JOIN team as t
      ON m.hometeam_id = t.team_api_id
      WHERE season = '2011/2012'
      GROUP BY team) AS subquery
```

Finally, order by home_avg, descending, and limit the query to 3 results

```sql
SELECT team, home_avg
FROM (SELECT
        t.team_long_name AS team
        AVG(m.home_goal) AS home_avg
      FROM match AS m
      LEFT JOIN team as t
      ON m.hometeam_id = t.team_api_id
      WHERE season = '2011/2012'
      GROUP BY team) AS subquery
ORDER BY home_avg DESC
LIMIT 3;
```

| team         | home_avg |
|--------------|----------|
| FC Barcelona | 3.84     |
| Real Madrid  | 3.68     |
| PSV          | 3.35     |

The final query returns top 3 teams based on home_goals scored in the 2011/2012 season

##### Things to remember
- Create multiple subqueries in one `FROM` statement
  - Alias them
  - Join them
- Join a subquery to a table in `FROM`
  - Include a joining columns in both tables