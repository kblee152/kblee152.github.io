---
layout: post
title: "Carsharing 데이터 분석 3: Cohort Analysis"
tags: [tableau, carsharing]
comments: true
---

Table: dump table

| 필드 이름 | 유형 |
|:---|:---|
| id  | INTEGER  |
| created  | TIMESTAMP  |
| updated  | TIMESTAMP  |
| deleted  | TIMESTAMP  |
| status  | INTEGER  |
| pickup_time  | TIMESTAMP  |
| return_time  | TIMESTAMP  |
| options  | INTEGER  |
| purpose  | STRING  |
| car_id  | INTEGER  |
| exemption_id  | STRING  |
| paycard_id  | STRING  |
| pickup_spot_id  | INTEGER  |
| return_spot_id  | INTEGER  |
| user_id  | INTEGER  |
|----

##### 전체 대여 횟수 및 이용자 확인

```sql
SELECT COUNT(id), COUNT(DISTINCT user_id)
FROM `carsharing-256705.carsharing.dump`
```

|   | count | user_count |
|---|-------|------------|
| 1 | 47011 | 2875       |