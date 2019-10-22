---
layout: post
title: "SQL Subqueries in FROM"
tags: [SQL]
comments: true
---

Datacamp `Intermediate SQL` Chapter_2_Short-and-Simple-Subqueries  
Subqueries in FROM 요약

subqueries in `WHERE` can only return a single column. if you want to return a more complex set of results, subquery in the `FROM` statement are a robust tool for restructuring and transforming your data. Subqueries in a `FROM` statement are a common way of preparing that data. Subqueries in `FROM` are also userful when calculating aggregates of aggregate information.

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


##### Practice 1: Joining Subqueries in FROM

1. Construct a subquery that selects only matches with 10 or more total goals
2. Inner join the subquery onto `country` in the main query
3. Select `name` from `country` and count the `id` column from `match`

  ```sql
  SELECT
    /* Selct country name and the count match IDs */
    c.name AS country_name,
    count(sub.id) AS matches
  FROM country AS c
  /* Inner join the subquery onto country */
  /* Select the country id and match id columns */
  INNER JOIN (SELECT country_id, id
              FROM match
              /* Filter the subquery by matches with 10+ goals */
              WHERE (home_goal + away_goal) >= 10) AS sub
  ON c.id = sub.country_id
  GROUP BY country_name;
  ```
The match table in the European Soccer Database does not contain country or team names. You can get this information by joining it to the country table, and use this to aggregate information, such as the number of matches played in each country.

If you're interested in filtering data from one of these tables, you can also create a subquery from one of the tables, and then join it to an existing table in the database. A subquery in FROM is an effective way of answering detailed questions that requires filtering or transforming data before including it in your final results.

Your goal in this exercise is to generate a subquery using the match table, and then join that subquery to the country table to calculate information about matches with 10 or more goals in total!

| country_name | matches |
|--------------|---------|
| Netherlands  | 1       |
| Spane        | 4       |
| Germany      | 1       |

