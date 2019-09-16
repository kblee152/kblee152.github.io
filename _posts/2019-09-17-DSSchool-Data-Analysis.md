---
layout: post
title: "(1)DSSchool Data Analysis"
tags: [SQL, DSSchool]
comments: true
---


## Level 1
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





