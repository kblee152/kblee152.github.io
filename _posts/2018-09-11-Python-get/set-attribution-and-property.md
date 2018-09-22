---
layout: post
title: "Python get/set attribution and property"
tags: [python]
comments: true
---

- `getter`와 `setter` 메서드는 객체의 변수(속성)을 읽고 변경하는데 사용
- 객체(Object) = 속성(Attribute) + 기능(Method)
- 파이썬의 속성과 메서드는 public
- getter, setter 메서드 대신 `property`를 사용

> 홑밑줄(single underscore): 내부적으로 사용하는 변수일 때 사용

> 곁밑줄(double underscore): 클래스 외부에서 접근할 수 없도록 내부 변수로 만듬

```python
class Duck():
    def __init__(self, input_name):
        self.hidden_name = input_name
    def get_name(self):
        print('inside the getter')
        return self.hidden_name
    def get_name(self):
        print('inside the setter')
        self.hidden_name = input_name
    name = property(get_name, set_name)

class Duck():
    def __init__(self, input_name):
        self.hidden_name = input_name
    @property
    def name(self):
        print('inside the getter')
        return self.hidden_name
    @name.setter
    def name(self, input_name):
        print('inside the setter')
        self.hidden_name = input_name
 ```       

```python
class C(object):
    def __init__(self, v):
        self.value = v
    def show(self):
        print(slef.value)
    def getValue(self):
        return self.value
    def setValue(self, v):
        self.value = v

c1 = C(10)
print(c1.getValue())
c1.setValue(20)
print(c1.getValue())
```


```python
class Cal(object):
    def __init__(self, v1, v2):
        self.v1 = v1
        self.v2 = v2
    def add(self):
        return self.v1 + self.v2
    def subtract(self):
        return self.v1 - self.v2
```

```python
c1 = Cal(10,10)
print(c1.add())
print(c1.subtract())
```

> 직접 변경 시도 시 오류 발생 가능, 문자열과 숫자의 연산 시도

```python
c1.v1 = 'one'
c1.v2 = 30
print(c1.add())
print(c1.subtract())
```

```python
class Cal(object):
    def __init___(self, v1, v2):
        isinstance(v1, int):
            self.v1 = v1
        isinstance(v2, int):
            self.v2 = v2
    def add(self):
        return self.v1 + self.v2
    def subtract(self):
        return self.v1 - self.v2
    def setV1(self, v):
        if isinstance(v, int):
            self.v1 = v
    def getV1(self):
        return self.v1

c1.setV1('one')
c1.v2 = 30
```
