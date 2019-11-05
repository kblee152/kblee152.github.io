---
layout: post
title: "Intermediate SQL Bring it all together(CASE, Subquery, Window Function"
tags: [Datacamp]
comments: true
---

#### Setting up the home team CTE

```sql
SELECT
    m.id,
    t.team_long_name,
    -- Identify matches as home/away wins or ties
    CASE WHEN m.home_goal > m.away_goal TEHN 'MU Win'
         WHEN m.home_goal < m.away_goal THEN 'MU Loss'
         ELSE 'Tie' END AS outcome
FROM match AS m
LEFT JOIN team AS t
ON m.hometeam_id = t.team_api_id
WHERE
    -- Filter for 2014/2015 and Manchester United as the home team
    m.season = '2014/2015'
    AND t.team_long_name = 'Manchester United';
```

#### Setting up the away team CTE

```sql
SELECT
    m.id,
    t.team_long_name,
    -- Identify matches as homw/away wins or ties
    CASE WHEN m.home_goal > m.away_goal THEN 'MU Loss'
         WHEN m.home_goal < m.away_goal THEN 'MU Win'
         ELSE 'Tie' END AS outcome
    
    -- Join team table to the match table
FROM match AS m
LEFT JOIN team AS t
ON m.awayteam_id = t.team_api_id
WHERE
    -- Filter for 2014/2015 and Manchester United as the away team
    m.season = '2014/2015'
    AND t.team_long_name = 'Manchester United';
```

#### Putting the CTEs together
Created the tow subqueries identifying the home and away team opponents, to rearrange your query with the `home` and `away` subqueries as Common Table Expressions. the main query includes the phrase, `SELECT DISTINCT`. without identifying only `DISTINCT` matches, you will return a duplicate record for each game played. 

```sql
-- Set up the home team CTE
WITH home AS (
    SELECT m.id, t.team_long_name,
        CASE WHEN m.home_goal > m.away_goal THEN 'MU Win'
             WHEN m.home_goal < m.away_goal THEN 'MU Loss'
             ELSE 'Tie' END AS outcome
    FROM match as m
    LEFT JOIN team AS t ON m.hometeam_id = t.team_api_id),

-- Set up the away team CTE
away AS (
    SELECT m.id, t.team_long_name,
        CASE WHEN m.home_goal > m.away_goal THEN 'MU Win'
             WHEN m.home_goal < m.away_goal THEN 'MU Loss'
             ELSE 'Tie' END AS outcome
    FROM match AS m
    LEFT JOIN team AS t ON m.awayteam_id = t.team_api_id)

-- Select team names, the date and goals
SELECT DISTINCT
    m.date,
    home.team_long_name AS home_team,
    away.team_long_name AS away_team,
    m.home_goal, m.away_goal
-- Join the CTEs onto the match table
FROM match AS m
LEFT JOIN home ON m.id = home.id
LEFT JOIN away ON m.id = away.id
WHERE m.season = '2014/2015'
    AND (home.team_long_name = 'Manchester United'
        OR away.team_long_name = 'Manchester United');
```

#### Add a window function 
