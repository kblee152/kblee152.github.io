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
