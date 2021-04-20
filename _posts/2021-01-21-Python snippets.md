---
layout: post
title: Pytorch snippets
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
```python
var foo = function(x) {
  return(x + 5);
}
foo(3)
```


## 자주 사용하는 코드 모음

```python
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

### Reference
**[1] [dl-pytorch-snippets](https://gaussian37.github.io/dl-pytorch-snippets/#dataloader%EC%9D%98-pin_memory-1)**  
**[2] [nn.Sequential() / nn.ModuleList()](https://gaussian37.github.io/dl-pytorch-snippets/#dataloader%EC%9D%98-pin_memory-1)**  
**[3] [nn.Embedding()](https://wikidocs.net/64779)** 

