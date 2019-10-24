---
layout: post
title: "SQL CASE WHEN"
tags: [SQL]
comments: true
---

`CASE WHEN`은 데이터 분석 시 많이 사용되는 문장으로 `집계 함수`와 `GROUP BY`절과 결합하면 데이터 분석에 유용하며 아래와 같이 구성된다.

```sql
SELECT 열 이름
    CASE WHEN [조건 1] THEN [결과 1]
         WHEN [조건 2] THEN [결과 2]
         ELSE [결과 3] END AS 열 이름
FROM 테이블명
```

##### Sample Table
CLERK는 7%, OFFICER는 5%, MANAGER는 3%의 연봉을 인상할 예정으로 예상 연봉을 NEXT_SAL column에 저장

| ID   | JOB     | CURRENT_SAL | NEXT_SAL |
|------|---------|-------------|----------|
| 1111 | OFFICER | 40,000      | 42,000   |
| 1112 | CLERK   | 32,000      | 32,240   |
| 1113 | MANAGER | 100,000     | 103,000  |

```sql
SELECT ID, JOB, CURRENT_SAL,
    CASE WHEN JOB = 'CLERK' THEN CURRENT_SAL * 1.07
         WHEN JOB = 'OFFICER' THEN CURRENT_SAL * 1.05
         WHEN JOB = 'MANAGER' THEN CURRENT_SAL * 1.03
         ELSE CURRENT_SAL END AS NEXT_SAL
FROM STAFF_SAL;
```

> CASE WHEN 함수에서 EQUAL 조건만 있을 경우 DECODE 함수를 사용할 수 있다

```sql
DECODE(열 이름, 조건 1, 결과 1
              조건 2, 결과 2
              조건 3, 결과 3, 기본 값) 새로운 열 이름
```

```sql
SELECT ID, JOB, CURRENT_SAL,
    DECODE(JOB, 'CLERK', CURRENT_SAL * 1.07,
                'OFFICER', CURRENT_SAL * 1.05,
                'MANAGER', CURRENT_SAL * 1.03, CURRENT_SAL) NEXT_SAL
FROM STAFF_SAL;
```
