---
layout: post
title: Python snippets
subtitle: 기본 문법, 자주사용하는 함수, 코드 모음
tags: [Settings, Python]
comments: true
---

## Table of contents
- [세팅 및 문법 관련](#세팅-및-문법-관련)
- [자주사용하는 함수](#자주사용하는-함수)
- [자주 사용하는 코드 모음](#자주-사용하는-코드-모음)  

## 세팅 및 문법 관련  
### Dictionary 관련 함수들
- d.items(), d.keys(), d.values(), d.get('key 값')  

```python
a = {'name': 'pey', 'phone': '0119993323', 'birth': '1118'}

>>> a.get('name')
'pey'

>>> a.items()
dict_items([('name', 'pey'), ('phone', '0119993323'), ('birth', '1118')])

>>> list(a.keys())
>>> ['name', 'phone', 'birth']

# 해당 Key가 딕셔너리 안에 있는지 조사하기
>>> 'name' in a
True

>>> 'email' in a
False
```

### heapq 모듈 / 힙(Heap) 구조
- heapq.heappush(list,value), heapq.heappop(list) : heapq는 일반적인 리스트와 다르게, 가지고 있는 요소를 push, pop 할때마다 자동으로 정렬해줌. 정렬 비용을 감소시킴으로써 효율성 이슈 해결
```python
h = []
for x in lst:
    heapq.heappush(h,x)
heapq.heappush(h, heapq.heappop(h) + (heapq.heappop(h) * 2))
```


### 문자열 치환 replace 함수  
- replace('검색 문자', '치환 문자', 바꿀횟수)  

```python
# 검색 문자 전부 변경하고 싶을 때
str = 'orange, orange, melon'
str = str.replace('orange', 'apple')
>>> apple, apple, melon

# 특정 횟수만큼 바꾸고 싶을 경우
str = 'orange, orange, melon'
str = str.replace('orange', 'apple', 1)
>>> apple, orange, melon
```

### 시작하는 문자 startswith  
- startswith('시작 문자')

```python
# 기본 예제
s = 'hello world'
s.startswith('hello')
>>> True

# 프로그래머스 예제
for p1, p2 in zip(phoneBook, phoneBook[1:]):
    if p2.startswith(p1):
```

## 자주사용하는 함수  
### Object의 속성(attribute) 존재를 확인하는 함수  
- `hasattr` / `getattr` / `setattr` : 멤버 확인, 변수 값 가져오기, 변수 값 설정  

```python
class cls:
    a = 1
    def b(self):
        pass

# cls에 b라는 멤버가 있는지 확인
>>> hasattr(cls, 'b')
True

# cls에서 a변수의 값 가져오기
>>> getattr(cls, 'a')
1

# cls의 a라는 변수에 값 9 설정하기
>>> setattr(cls, 'a', 9)
```


## 자주 사용하는 코드 모음
### iterable 자료형을 순서대로 묶어주는 zip 함수  
- 배열을 같은 인덱스끼리 짝지어준다. 만약 배열의 길이가 다를 경우 같은 인덱스끼리만 짝지어주고, zip 객체에서 나머지 인덱스는 제외된다  

```python
participant.sort()
completion.sort()

for p,c in zip(participant, completion):
    if p != c:
        return p
return participant.pop()
```


### Reference
**[1] [파이썬 조각 코드 모음집](https://wikidocs.net/book/536)**  



