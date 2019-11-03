---
layout: post
title: "SQL 윈도 프레임 지정"
tags: [SQL]
comments: true
---

##### 윈도 프레임 지정
`ORDER BY`구문과 `SUM/AVG`등의 집약 함수를 조합하면, 집약 함수의 적용 범위를 유연하게 지정할 수 있음. 프레임 지정이란 현재 레코드 위치를 기반으로 상대적인 윈도를 정의하는 구문. 가장 기본적으로 `ROWS BETWEEN start ADN edn`, start와 end에는 `CURRENT ROW`, `n PRECEDING`, `n FOLLOWING`, `UNBOINDED PRECEDING`, `UNBOUNDED FOLLOWING` 등의 키워드를 지정. 

```sql
SELECT
    product_id,
    score,

    -- 점수 순서로 유일한 순위를 붙임
    ROW_NUMBER() OVER(ORDER BY score DESC) AS row,

    --  순위 상위부터의 누계 점수 계산
    SUM(score)
        OVER(ORDER BY score DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS cum_score,

    -- 현재 행과 앞 뒤의 행이 가진 값을 기반으로 평균 점수 계산
    AVG(score)
        OVER(ORDER BY score DESC
            ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)
    AS local_avg,

    -- 순위가 높은 상품 ID 추출
    FIRST_VALUE(product_id)
        OVER(ORDER BY score DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
    AS fisrt_value

    -- 순위가 낲은 상품 ID 추출
    LAST_VALUE(product_id)
        OVER(ORDER BY score DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
    AS last_value
FROM popular_products
ORDER BY row
;
```

| product_id | score | row | cum_score | local_avg | first_value | last_value |
|------------|-------|-----|-----------|-----------|-------------|------------|
| A001       | 94    | 1   | 94        | 92.00     | A001        | D004       |
| D001       | 90    | 2   | 184       | 88.67     | A001        | D004       |


WINDOW FRAME
: 파티션 내의 시작점 및 끝점을 지정하여 파티션 내의 행을 추가로 제한. 논리적 연결이나 물리적 연결을 통해 현재 행을 기준으로 한 행 범위를 지정하여 수행. 물리적 연결은 ROW 절을 사용하여 수행

ROW절
: 현재 행 이전 또는 다음의 고정 행 수를 지정하여 파티션 내의 행 수를 제한. ROW 절에는 ORDER BY절을 지정해야함  




```sql
SELECT
    product_id,
   
    -- 점수 순서로 유일한 순위 선정
    ROW_NUMBER() OVER(ORDER BY score DESC) AS row,

    -- 가장 앞 순위부터 가장 뒷 순위까지의 범위를 대상으로 상품 ID 집약
    array_agg(product_id)
        OVER(ORDER BY score DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
    AS whole_agg

    -- 가장 앞 순위부터 현재까지의 범위를 대상으로 상품 ID 집약
    array_agg(product_id)
        OVER(ORDER BY score DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS cum_agg

    -- 순위 하나 앞과 하나 뒤까지의 범위를 대상으로 샹품 ID 집약
    array_agg(product_id)
        OVER(ORDER BY score DESC
            ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)
    AS local_agg 
    FROM popular_products
    WHERE category = 'action'
    ORDER BY row
    ;
    ```

> 윈도 함수에 프레임 지정을 하지 않으면 ORDER BY 구문이 없는 경우 모든 행, ORDER BY 구문이 있는 경우 **첫 행에서 현재 행**까지가 디폴트 프레임으로 지정
