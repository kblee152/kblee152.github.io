---
layout: post
title: "SQL Window Functions"
tags: [SQL]
comments: true
---

##### Working with aggregate values
- Requires you to use `GROUP BY` with **all** non-aggregate columns

If you try to retrieve additional information without grouping by every single non-aggregate value, query will return an error

> NOTE: GROUP BY 구문을 사용한 쿼리에서는, GROUP BY 구문에 지정한 컬럼 또는 집약 함수만 SELECT 구문의 컬럼으로 지정할 수 있다. 참고로, GROUP BY 구문을 사용한 쿼리에서는 GROUP BY 구문에 지정한 컬럼을 유니크 키로 새로운 테이블을 생성하고, 이 과정에서 GROUP BY 구문에 지정하지 않은 컬럼은 사라진다. 따라서 집약 함수를 적용한 값과 집약 전의 값은 동시에 사용할 수 없다.

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
  - Running totals, rankings, moving averages

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

- ROW_NUMBER: 순서에 유일한 순위 번호를 붙임
- DENSE_RANK: 같은 순위의 레코드에 같은 순위 번호를 붙임
- RANK: 같은 순위의 레코드에 같은 순위 번호를 붙이고 뒤의 순위 번호를 건너 뜀
- LAG: 기준 행의 앞 행 추출
- LEAD: 기준 행의 뒤 행 추출

##### Key Differences
- Processed after every part of query except `ORDER BY`
  - Uses information in result set rather than database
- Available in PostgreSQL, Oracle, MySQL, SQL Server...
  - ...Not SQLite

> NOTE: 집약 함수로 윈도 함수를 사용하려면, 집약 함쉬 뒤에 OVER 구문을 붙이고 여기에 윈도 함수를 지정한다. OVER 구문에 매개 변수를 지정하지 않으면 테이블 전체에 집약 함수를 적용한 값이 리턴된다. 매개 변수에 PARTITION BY <COLUMN>을 지정하면 해당 컬럼 값을 기반으로 그룹화하고 집약 함수를 적용한다.

```sql
SELECT 
    user_id,
    product_id,
    -- 개별 점수 리뷰
    score,
    -- 전체 점수 리뷰
    AVG(score) OVER() AS avg_score,
    -- 사용자의 평균 리뷰 점수
    AVG(score) OVER(PARTITION BY user_id) AS user_avg_score,
    -- 개별 리뷰 점수와 사용자 평균 리뷰 점수의 차이
    score - AVG(score) OVER(PARTITION BY user_id) AS user_avg_score_diff
FROM
    review;
```

