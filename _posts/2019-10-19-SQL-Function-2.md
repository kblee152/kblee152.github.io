---
layout: post
title: "SQL 숫자데이터 요약"
tags: [SQL]
comments: true
---

| 함수     | 설명          | 비고                                                                          |
|----------|---------------|----------------------------------------------------------------------------------------|
| COUNT    | 행의 수       | NULL 값 포함: COUNT(*) / NULL 값 제외: COUNT(열 이름)  / 중복 제외: COUNT(DISTINCT 열 이름) |
| SUM      | 행의 합계     |                                                                                        |
| AVG      | 행의 평균     |                                                                                        |
| MAX      | 행의 최댓값   |                                                                                        |
| MIN      | 행의 최솟값   |                                                                                        |
| STDENV   | 행의 표준편차 |                                                                                        |
| VARIANCE | 행의 분산     |

> COUNT 함수는 데이터 검증용으로 많이 사용된다. NULL 값, 중복 값 등을 체크한다.

> 집계 함수를 사용하면 NULL 값은 계산에서 무시된다. 예로 AVG 함수를 사용하면 NULL 값이 무시되며 NULL 값을 포함해서 계산하고 싶다면 아래와 같이 COALESCE 함수를 이용하여 치환한다.

```sql
SELECT AVG(COALESCE(SCORE, 0)) AS SCORE_AVG
FROM SCORE_TABLE;
```

> 또한 숫자형 데이터를 분석할 때 SUM, AVG, MIN, MAX 값을 사용하여 데이터를 검증하는 것이 중요하다.