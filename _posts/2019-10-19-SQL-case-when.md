---
layout: post
title: "SQL CASE WHEN"
tags: [SQL]
comments: true
---


##### In CASE you need to aggregate
`CASE` statements are great for
- Categorizing data
- Filtering data
- Aggregating data

##### CASE WHEN with COUNT

```sql
SELECT 
    season,
    COUNT(CASE WHEN hometeam_id = 8650
    AND home_goal > away_goal
    THEN id END) AS home_wins
FROM match
GROUP BY season;
```

```sql
SELECT
    season,
    COUNT(CASE WHEN hometeam_id = 8650 AND home_goal > away_goal
          THEN id END) AS home_wins
    COUNT(CASE WHEN awayteam_id = 8860 AND away_goal > home_goal
          THEN id END) AS away_wins
FROM match
GROUP BY season;
```

| season    | home_wins | away_wins |
|-----------|-----------|-----------|
| 2001/2012 | 6         | 8         |
| 2012/2013 | 9         | 7         |
| 2013/2014 | 16        | 10        |



##### Percentages with CASE and AVG

The question we're answering here is,  
"What percentage of Liverpool's games did they win in each season?"

```sql
SELECT
    season,
    AVG(CASE WHEN hometeam_id = 8455 AND home_goal > away_goal THEN 1
             WHEN hometeam_id = 8455 AND home_goal < away_goal THEN 0
             END) AS pct_homewins,
    AVG(CASE WHEN awayteam_id = 8455 AND away_goal > home_goal THEN 1
             WHEN awayteam_id = 8445 AND away_goal < home_goal THEN 0
             END) AS pct_awaywins
FROM match
GROUP BY season;
```

| season    | pct_homewins | pct_awaywins |
|-----------|--------------|--------------|
| 2011/2012 | 0.75         | 0.5          |
| 2012/2013 | 0.86         | 0.67         |
| 2013/2014 | 0.94         | 0.67         |