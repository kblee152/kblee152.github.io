---
layout: post
title: "DS-School Level 1 Pandas Series, Nan"
tags: [DSSchool]
comments: true
---

#### pandas Series

```python
import pandas as pd

odd = [1, 3, 5, 7, 9]

pd_odd = pd.Series(odd)
print(pd_odd)
```

pandas Series는 python의 list와 유사한 형태로,  
pandas Series로 사용해야 pandas의 기능을 사용할 수 있음

pd.Series() 함수를 사용하며, python의 list, numpy의 array가 인자로 입력 

`.values`: value를 array로 확인  
`.index`: index의 범위값 확인

```python
pd_odd.values
pd_odd.index
```

Series의 index 설정
```python
pd.Series(odd, index = ['a', 'b', 'c', 'd', 'e'])
```
Series의 이름 설정
```python
pd.Series.name = series 이름
```
Series index의 이름 설정
```python
pd.Series.index.name = index 이름
```
Series의 index 값 변경
```python
pd_odd.index = ['1', '2', '3', '4', '5']
```

```python
pd_odd.mean()
pd_odd.sum()
pd_odd.describe()
```



### Nan(Not a Number)

```python
import numpy as np

odd = [1, 3, 5, 7, 9]
odd = pd.Series(odd)
odd.dtypes

# dtype('int64')

odd = [1, 3, 5, 7, 9, np.nan]
odd.dtypes

# dtype('float64')
```

데이터 분석 시 의미 없는 값은 Nan으로 처리 필요  
키, 몸무게 분석 등에 음수 값이 표함된 경우 등
