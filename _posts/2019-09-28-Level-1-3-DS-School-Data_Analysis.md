---
layout: post
title: "DS-School Level 1 Pandas File 읽기"
tags: [DSSchool]
comments: true
---

#### Pandas File 읽기

```python
import pandas as pd

order_url = 'https://sampleUrl.com'
pd.read_csv(order_url)
```

| | id | user_id | product_id | date | price | address | state |
|:-----|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0  | 1  | 3  | 9  | 2017-01-01  | 500  | Seoul  | confirmed  |
| 1  | 2  | 1  | 7  | 2017-01-03  | 700  | Seoul  | canceled  |
|----

#### Pandas Index 설정

- Column: id, user_id, product_id, ... , (Column을 나타내는 부분)
- Index: 0, 1, 2, 3, 4, 5, ... , (Row를 나타내는 부분))

```python
order_url = 'https://sampleUrl.com'
order = pd.read_csv(order_url)
order = order.set_index('id')
order
```

| id | user_id | product_id | date | price | address | state |
|:-----|:----:|:----:|:----:|:----:|:----:|:----:|
| 1  | 3  | 9  | 2017-01-01  | 500  | Seoul  | confirmed  |
| 2  | 1  | 7  | 2017-01-03  | 700  | Seoul  | canceled  |
|----

#### Pandas Columns 설정

```python
# Column 설정
order.columns = ['user_id', 'product_id', 'date', 'price', 'state']
# Column 출력
order.columns
```

#### Pandas Data 출력

```python
# 상위 데이터 출력
order.head()
# 특정 개수의 상위 데이터 출력
order.head(3)
#하위 데이터 출력
order.tail()
# 특정 개수의 하위 데이터 출력
order.tail(3)
```

