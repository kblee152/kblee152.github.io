---
layout: post
title: "Intermediate Python: Basic plot with matplotlib"
tags: [Datacamp]
comments: true
---

#### Data Visualization
- Very important in Data Analysis
  - Exlore data
  - Report insights

```sql
import matplotlib.pyplot as plt

year = [1950, 1970, 1990, 2010]
pop = [2.519, 3.692, 5.263, 6.972]

plt.plot(year, pop)
plt.show()
```

![Image-1](../images/2019-11-07-Python-dc-basic-plots-with-matplotlib-1.png){: .center-image}

#### Scatter plot

```sql
import matplotlib.pyplot as plt

year = [1950, 1970, 1990, 2010]
pop = [2.519, 3.692, 5.263, 6.972]

plt.scatter(year, pop)
plt.show()
```
![Image-1](../images/2019-11-07-Python-dc-basic-plots-with-matplotlib-2.png){: .center-image}

#### Histogram
- Explore dataset
- Get idea about distribution

![Image-1](../images/2019-11-07-Python-dc-basic-plots-with-matplotlib-3.png){: .center-image}

![Image-1](../images/2019-11-07-Python-dc-basic-plots-with-matplotlib-4.png){: .center-image}

```python
import matplotlib.pyplot as plt

values = [0, 0.6, 1.4, 1.6, 2.2, 2.5, 2.6, 3.2, 3.5, 3.9, 4.2, 6]
plt.his(values, bins = 3)
plt.show()
```
![Image-1](../images/2019-11-07-Python-dc-basic-plots-with-matplotlib-5.png){: .center-image}

