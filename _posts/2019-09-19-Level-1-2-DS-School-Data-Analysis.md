---
layout: post
title: "DS-School Level 1-2 DataFrame 생성하기"
tags: [SQL, DSSchool]
comments: true
---

### DataFrame 생성 - 1

```python
import pandas as pd

order = [
    ['2017-01-01', 500, 'confirmed']
    ['2017-01-03', 700, 'confirmed']
    ['2017-01-10', 200, 'canceled']
]

order = pd.DataFrame(order)
order
```

Column 값을 명시할 수 없기때문에 별도로 Column 값 지정 필요

```python
columns = ['data', 'price', 'state']
order = pd.DataFrame(order, columns = columns)
order
```

### DataFrame 생성 - 2

```python
import pandas as pd

order = {
    'date': ['2017-01-01', '2017-01-03', '2017-01-10'],
    'price': [500, 700, 200],
    'state': ['confirmed', 'confirmed', 'canceled']
}

order = pd.DataFrame(order)
order
```

### DataFrame 생성 - 3

```python

import pandas as pd

order = [
    {'date': '2017-01-01', 'price': 500, 'state': 'confirmed'},
    {'date': '2017-01-03', 'price': 700, 'state': 'confirmed'},
    {'date': '2017-01-10', 'price': 200, 'state': 'canceled'},
]

order = pd.DataFrame(order)
order
```
