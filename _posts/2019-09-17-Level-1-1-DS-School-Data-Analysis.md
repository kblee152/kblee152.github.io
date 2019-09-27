---
layout: post
title: "DS-School Level 1-1 Pandas Series, DataFrame, Non"
tags: [DSSchool]
comments: true
---

### pandas Series and DataFrame

```python
import pandas as pd

pd_odd = pd.Series(odd)
print(pd_odd)
```
pandas Series는 python의 list와 유사한 기능  
pandas Series로 사용해야 pandas의 기능을 사용할 수 있음

```python
pd_odd.mean()
```


```python
numbers = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

numbers = pd.DataFrame(numbers)
print(numbers)
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

