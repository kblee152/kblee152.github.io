---
layout: post
title: "Pandas 자료구조: Series"
tags: [Pandas]
comments: true
---

##### Series
Series는 일련의 객체를 담을 수 있는 1차원 배열 같은 자료구조로 색인(index)이라는 배열의 데이터와 연관된 이름을 가지고 있음.


```python
import pandas as pd

obj = pd.Series([4, 7, -5, 3])
obj
```




    0    4
    1    7
    2   -5
    3    3
    dtype: int64



왼쪽에 색인을 보여주고, 오른쪽에 해당 색인의 값을 보여주며, 데이터의 색인을 지정하지 않을 경우 정수 0에서 N-1(데이터의 길이)까지의 숫자가 표시


```python
obj.values
```




    array([ 4,  7, -5,  3])




```python
obj.index
```




    RangeIndex(start=0, stop=4, step=1)



각각의 데이터를 지칭하는 색인을 지정하여 Series 객체 생성 시


```python
obj2 = pd.Series([4, 7, -5, 3], index = ['d', 'b', 'a', 'c'])
obj2
```




    d    4
    b    7
    a   -5
    c    3
    dtype: int64




```python
obj2.index
```




    Index(['d', 'b', 'a', 'c'], dtype='object')



Numpy 배열과 비교 시, 단일 값을 선택하거나 여러 값을 선택할 때 색인으로 라벨을 사용할 수 있음


```python
obj2['a']
```




    -5




```python
obj2['d']
```




    4




```python
obj2[['c', 'a', 'd']]
```




    c    3
    a   -5
    d    4
    dtype: int64



**불리언 배열을 사용해서 값을 필터링, 산술 곱셈, 수학 함수를 적용하는 등 Numpy 배열 연산을 수행해도 색인-값 연결이 유지**


```python
obj2[obj2 > 0]
```




    d    4
    b    7
    c    3
    dtype: int64




```python
obj2 * 2
```




    d     8
    b    14
    a   -10
    c     6
    dtype: int64




```python
'b' in obj2
```




    True



Series 객체 생성: 사전형 데이터(Dictionary)


```python
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}
obj3 = pd.Series(sdata)
obj3
```




    Ohio      35000
    Texas     71000
    Oregon    16000
    Utah       5000
    dtype: int64



이 경우 Series 객체의 색인에는 사전의 키값이 순서대로 입력되며 색인을 직접 지정하고 싶다면 아래와 같이 원하는 순서대로 색인을 넘겨줄 수 있음


```python
states = ['California', 'Ohio', 'Oregon', 'Texas']
obj4 = pd.Series(sdata, index = states)
obj4
```




    California        NaN
    Ohio          35000.0
    Oregon        16000.0
    Texas         71000.0
    dtype: float64



이 경우 'California'에 대한 값은 찾을 수 없기 때문에 NaN(Not a number)으로 표기

Pandas에서 누락된 데이터 확인: isnull(), notnull()


```python
pd.isnull(obj4)
```




    California     True
    Ohio          False
    Oregon        False
    Texas         False
    dtype: bool




```python
pd.notnull(obj4)
```




    California    False
    Ohio           True
    Oregon         True
    Texas          True
    dtype: bool




```python
obj4.isnull()
```




    California     True
    Ohio          False
    Oregon        False
    Texas         False
    dtype: bool



Series는 산술 연산 시 색인과 라벨을 자동 정렬함


```python
obj3 + obj4
```




    California         NaN
    Ohio           70000.0
    Oregon         32000.0
    Texas         142000.0
    Utah               NaN
    dtype: float64



Series 색인의 name 속성


```python
obj4.name = 'population'
```


```python
obj.index.name = 'state'
```


```python
obj4
```




    California        NaN
    Ohio          35000.0
    Oregon        16000.0
    Texas         71000.0
    Name: population, dtype: float64



Series의 색인은 대입하여 변경 가능


```python
obj
```




    state
    0    4
    1    7
    2   -5
    3    3
    dtype: int64




```python
obj.index = ['Bob', 'Steve', 'Jeff', 'Ryan']
obj
```




    Bob      4
    Steve    7
    Jeff    -5
    Ryan     3
    dtype: int64


