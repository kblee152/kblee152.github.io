---
layout: post
title: "Carsharing 데이터 분석 4: 재예약 분포"
tags: [data-analysis]
comments: true
---

멤버십, 정기 구독 상품 등이 아닌 경우 해당 고객이 언제 다시 서비스를 이용할지, 완전히 이탈한 것인지 명확히 확인이 어려움. 카셰어링의 주요 고객층이 `20대 초반`, `여가 목적 활용`, `이탈 시점 파악이 어려움(취업 등의 생활 패턴 변화, 차량 구매 등)` 등을 단순 가정하고 재사용 기간에 대한 분석. **(주의: 개인 기록용으로 잘못된 정보를 다수 포함할 수 있음)**

```python
import pandas as pd
import numpy as np
```

##### 데이터 불러오기

```python
raw_data = pd.read_csv("dump.csv")
print(raw_data.shape)
raw_data.head()
```

```python
# 데이터 타입 변경
raw_data["pickup_time"] = pd.to_datetime(raw_data["pickup_time"])
raw_data["return_time"] = pd.to_datetime(raw_data["return_time"])

# 데이터 확인
print(raw_data.shape) # prints out 47011
print(raw_data['user_id'].unique().shape) # prints out 2875
```

##### 다음 대여 시간을 컬럼 추가하기
```python
raw_data.loc[raw_data.groupby('user_id')['pickup_time'].shift(-1), 'pickup_time_after']
raw_data.sort_values(by = ['user_id', 'pickup_time']).head()
```

##### 다음 예약까지의 기간 구하기
```python
raw_data['next_booking_period'] = raw_data['pickup_time_after'] - raw_data['pickup_time']
raw_data['next_booking_period'] = raw_data['next_booking_point'].fillna(0)
raw_data['next_booking_period'] = raw_data['next_bookingperiod'].dt.total_seconds().astype(float)
```

##### boxplot으로 시각화하기