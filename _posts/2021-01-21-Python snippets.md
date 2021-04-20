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
### block을 쌓기 위한 Module  
- `nn.Sequential` 여러 nn.Module을 한 컨테이너에 넣고 한번에 돌리는 방법. 컨테이너에 적힌 순서대로 값을 전달해 처리. 빠르고 간단히 사용하기 편함

```python
class MyModule(nn.Module):
    def __init__(self):
        super(MyModule, self).__init__()
        self.linears = nn.ModuleList([nn.Linear(10, 10) for i in range(10)])
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
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

### Reference
**[1] [파이썬 조각 코드 모음집](https://wikidocs.net/book/536)**  



