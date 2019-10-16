---
layout: post
title: "DS-School Level 1 Pandas 검색/색인"
tags: [DSSchool]
comments: true
---
##### Table: order

| id | user_id | product_id | date       | price | address | state     |
|----|---------|------------|------------|-------|---------|-----------|
| 1  | 3       | 9          | 2017-01-01 | 500   | Seoul   | confirmed |
| 2  | 1       | 7          | 2017-01-03 | 700   | Seoul   | confirmed |
| 3  | 3       | 8          | 2017-01-03 | 900   | Daejeon | confirmed |
| 4  | 4       | 2          | 2017-01-07 | 500   |         | canceled  |
| 5  | 7       | 3          | 2017-01-09 | 700   | Incheon | confirmed |
| 6  | 5       | 7          | 2017-01-09 | 600   | Busan   | canceled  |
| 7  | 2       | 5          | 2017-01-10 | 200   |         | canceled  |

##### Column 검색
```python
order["date"]
order[["user_id", "date", "amount"]]

columns = ["user_id", "date", "amount"]
order[columns]
```


##### Row 검색
```python
# loc = locate
order.loc
order.loc[1]
order.loc[[1, 3, 7]]

order_ids = [1, 3, 7]
order.loc[order_ids]

type(order.loc[[1, 3, 7]])
# pandas.core. frame.DataFrame
```

##### Row/Column 검색

```python
order_date = order.loc[1]["date"]
order_date

%timeit order.loc[1]["date"]
```

```python
order_date = order.loc[1, "date"]
order_date

%timeit order.loc[1, "date"]
```

##### Row/Column 검색: at, loc
- pandas at이 loc보다 속도가 빠름  
- at은 row, column 모두 하나씩만 접근 가능

```python
order.at[1, "date"]
```

##### 색인

```python
order["date"] == "2017-01-03"
```

| id |       |
|----|-------|
| 1  | False |
| 2  | True  |
| 3  | True  |
| 4  | False |

```python
order[order["date"] == "2017-01-03"]
```

|    | user_id | product_id | date       | price | address | state     |
|----|---------|------------|------------|-------|---------|-----------|
| id |         |            |            |       |         |           |
| 2  | 1       | 7          | 2017-01-03 | 700   | Seoul   | confirmed |
| 3  | 3       | 8          | 2017-01-03 | 900   | Daejeon | confirmed |


```python
order["price"] >= 500
```

| id |      |
|----|------|
| 1  | True |
| 2  | True |
| 3  | True |


```python
order[order["price"] >= 500]
```

|    | user_id | product_id | date       | price | address | state     |
|----|---------|------------|------------|-------|---------|-----------|
| id |         |            |            |       |         |           |
| 1  | 3       | 9          | 2017-01-01 | 500   | Seoul   | confirmed |
| 2  | 1       | 7          | 2017-01-03 | 700   | Seoul   | confirmed |


##### 다중조건

```python
(order["price"] >= 500) & (order["state"] == "confirmed")
```

| id |      |
|----|------|
| 1  | True |
| 2  | True |


```python
order[(order["price"] >= 500) & (order["state"] == "confirmed")]
```
| id |      |
|----|------|
| 1  | True |
| 2  | True |


```python
high = (order["price"] >= 500)
confirmed = (order["state"] == "confirmed")
order[high & confirmed]
```

| id |      |
|----|------|
| 1  | True |
| 2  | True |


```python
order.loc[order["date"] == "2017-01-09", "price"]
```

```python
order.loc[order["date"] == "2017-01-09", ["date", "price"]]
```