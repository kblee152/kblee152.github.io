---
layout: post
title: "Pandas Data Cleaning"
tags: [Pandas]
comments: true
---

##### Sample 1
Table: payments
결제가 완료된 경우 True, 아닌 경우 False인 컬럼 생성

|   | 상태      |
|---|-----------|
| 0 | 결제 완료 |
| 1 | 결제 완료 |
| 2 | 결제 완료 |

```python
payments['상태(bool)'] = (payments['상태'] == '결제 완료')
payments[['상태', '상태(bool)']].head()
```

|   | 상태      | 상태(bool) |
|---|-----------|------------|
| 0 | 결제 완료 | True       |
| 1 | 결제 완료 | True       |
| 2 | 결제 완료 | True       |

##### Sample 2

##### Sample 3

##### Sample 4
