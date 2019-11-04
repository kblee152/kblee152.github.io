---
layout: post
title: "Intermediate SQL Common Table Expressions"
tags: [Datacamp, SQL]
comments: true
---

##### When adding subqueries...
- Query complexity increases quickly
  - Information can be difficult to keep track of

common method for improving readablility and accessibility of imformation in subquery 

##### Common Table Expressions
- Common Table Expressions(CTEs)
- Table declared before the main query
- Named and referenced later in `FROM` statement

```sql
WITH cte AS (
    SELECT col1, col2
    FROM table)
SELECT 
    AVG(col1) AS avg_col
FROM cte;
```
Instead of wrapping subquery inside, name it using the `WITH` statement and then reference it by name later in the `FROM` statement as if it were any other table in your database.

##### Take a subquery in FROM
```sql
SELECT
    c.name AS country,
    COUNT(s.id) AS matches
FROM country AS c
INNER JOIN (
    SELECT country.id, id
    FROM match
    WHERE (home_goal + away_goal) >= 10) AS s
ON c.id = s.country_id
GROUP BY country;
```
##### Place it at the beginning
```sql
(
    SELECT country_id, id
    FROM match
    WHERE (home_goal + away_gola) >= 10
)
```

subquery, simply take the subquery out of the `FROM` clause, place it at the beginning of query. declare it using the syntax `WITH`, followd by a CTE name, and AS

```sql
WITH s AS (
    SELECT country_id, id
    FROM match
    WHERE (home_goal + away_goal) >= 10
)
```

##### Shw me the CTE
```sql
WITH s AS (
    SELECT country_id, id
    FROM match
    WHERE (home_goal + away_goal) >= 10
)
SELECT c.name AS country,
       COUNT(s.id) AS matches
FROM country AS c
INNER JOIN s
ON c.id = s.country_id
GROUP BY country;
```

##### Why use CTE?
Common table expressions have numerous benefits over a subquery written inside your main query
- Excuted once
  - CTE is then stored in memory
  - Improves query performance
- Improving organization of queries
- Referencing other CTEs
- Referencing itself(`SELF JOIN`)

