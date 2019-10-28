---
layout: post
title: "Pandas matplotlib plus figures axes and subplots"
tags: [Pandas]
comments: true
---

```python
import pandas as pd
df = pd.read_csv("../documents/dp_live.csv")
df.head(3)
```

```python
new_columns = [
    "country",
    "indicator",
    "subject",
    "measure",
    "frequency",
    "year",
    "value",
    "flag codes"
]

df.columns = new_columns
df.head(5)
```

```python
df["year"] = pd.to_datetime(df["year"])
df["year(clean)"] = df["year(clean")].dt.year
```


```python
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

sns.lineplot(data = df, x = "year(clean)", y = "value", hue = "country", estimator = np.sum)
```
