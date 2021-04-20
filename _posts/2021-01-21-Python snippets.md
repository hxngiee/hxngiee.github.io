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
### subject  
- `Keyword` content

```python
write code here
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

```python
write code here
```

### Reference
**[1] [파이썬 조각 코드 모음집](https://wikidocs.net/book/536)**  



