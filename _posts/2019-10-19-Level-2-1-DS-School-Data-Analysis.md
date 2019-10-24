---
layout: post
title: "DS-School Level 2 Pandas Pivot Table"
tags: [DSSchool]
comments: true
---

#### Parameters

- `data`: DataFrame
- `values`: 분석할 데이터 프레임 / column to aggregate, optional
- `index`: 행 인덱스로 들어갈 키 열 또는 키 열의 리스트 / column, Grouper, array, or list of th previous
- `columns`: 열 인덱스로 들어갈 키 열 또는 키 열의 리스트 / column, Grouper, array, or list of th previous
- `aggfunc`: function, list of functions, dict, default numpy.mean
- `fill_value`: Nan 대체 값 / scalar, default False
- `margins`: boolean, default False
- `dropna`: boolean, default True
- `margins_name`: string, dafault 'All'
- `observed`: boolean, default False