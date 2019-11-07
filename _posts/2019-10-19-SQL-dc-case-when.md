---
layout: post
title: "Intermediate SQL CASE WHEN"
tags: [Datacamp]
comments: true
---

##### CASE statements
- Contains a `WHEN`, `THEN`, and `ELSE` statement, finished with `END`

```sql
CASE WHEN x = 1 THEN 'a'
     WHEN x = 2 THEN 'b'
     ELSE 'c' END AS new_column
```

#### CASE WHEN ...AND then some
- Add multiple logical conditions to your `WHEN` clause
```sql
SELECT date, hometeam_id, awayteam_id,
    CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
            THEN 'Chelsea home win'
         WHEN awayteam_id = 8455 AND home_goal < away_goal
            THEN 'Chelsea away win'
         ELSE 'Loss or tie'
FROM match
WHERE hometeam_id = 8455 OR awayteam_id = 8455;
```

All other matches are categorized as a loss or tie.

| date       | hometeam_id | awayteam_id | outcome          |
|------------|-------------|-------------|------------------|
| 2011-08-14 | 10194       | 8455        | Loss or tie      |
| 2011-08-20 | 8455        | 8659        | Chelsea home win |

#### What ELSE is being excluded?
- What's in your `ELSE` clause?

Here's the same CASE statement from the previous slide, but the WHERE filter has been removed. Without this filter, ELSE clause will categorize ALL matches played by anyone, who don't meet these first two conditions, as Loss or tie.

```sql
SELECT date, hometeam_id, awayteam_id,
    CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
            THEN 'Chelsea home win'
         WHEN awayteam_id = 8455 AND home_goal < away_goal
            THEN 'Chelsea away win'
         ELSE 'Loss or tie'
FROM match
```

| date       | hometeam_id | awayteam_id | outcome     |
|------------|-------------|-------------|-------------|
| 2011-07-29 | 1773        | 8635        | Loss or tie |
| 2011-07-30 | 9998        | 9985        | Loss or tie |

#### What's NULL?
It's important to consider what your `ELSE` clause is doing
- 



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