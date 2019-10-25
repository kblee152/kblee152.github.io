---
layout: post
title: "SQL GROUP BY and HAVING"
tags: [SQL]
comments: true
---

특정한 테이블에서 특정한 조건을 만족하는 데이터를 추출한 후 특정한 조건을 만족한 그룹화된 특정 열 및 집계함수를 나타냄. 원하는 행을 필터링할 때는 `WHERE` 조건절, 행이 아닌 그룹화된 변수에 대해 필터링할 경우에는 `HAVING`을 사용함. **WHWERE 조건절의 조건은 데이터가 그룹화되기 전에 필터링하고, HAVING절의 조건은 데이터가 그룹화된 후 필터링함** 즉, WHERE 조건절에 의해 1차 필터링된 대상을 그룹화하여 HAVING절이 2차 필터링하는 것임. 그룹화하면 데이터를 논리적 집합으로 나누어서 데이터의 특성을 요약할 수 있음.

Sample Table: PPC_MAST_201312

| SSN       | ACCT_NO | ACCT_CD | PRFT | BALANCE_AMT |
|-----------|---------|---------|------|-------------|
| 123456789 | 1234    | 130     | 504  | 56000       |
| 987654321 | 4321    | 300     | 240  | 23534       |

- ACCT_CD(수신): 100, 110, 120, 130, 140
- ACCT_CD(여신): 300, 310, 320, 330, 340

위 테이블에서 자산과 부채를 구할경우 쿼리는 아래와 같음 

```sql
SELECT CASE WHEN ACCT_CD IN (100, 110, 120, 130, 140) THEN 'LIABLLITY'
            WHEN ACCT_CD IN (300, 310, 320, 330, 340) THEN 'ASSET'
        END AS BALLANCE_SHHET,
        SUM(BALANCE_AMT) AS total_BALANCE_AMT
FROM PPC_MAST_201312
GROUP BY BALLANCE_SHEET
ORDER BY BALLANCE_SHEET;
```

| BALANCE_SHEET | TOTAL_BALANCE_AMT |
|---------------|-------------------|
| ASSET         | 9909200           |
| LIABILITY     | 38020000          |