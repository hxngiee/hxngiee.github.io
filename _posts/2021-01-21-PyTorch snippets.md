---
layout: post
title: Pytorch snippets
subtitle: 기본 문법, 자주사용하는 함수, 코드 모음
tags: [Settings, PyTorch]
comments: true
---

## Table of contents
- [세팅 및 문법 관련](#세팅-및-문법-관련)
- [자주사용하는 함수](#자주사용하는-함수)
- [자주 사용하는 코드 모음](#자주-사용하는-코드-모음)  

## 세팅 및 문법 관련  
### torch.no_grad()와 model.eval()
- `torch.no_grad()` autograd engine을 꺼버려 더 이상 자동으로 gradient를 트래킹하지 않는다. 메모리 사용량을 줄이고 연산 속도를 높히기 위해 사용되며 inference 진행할때 torch.no_grad() with statement로 감싼다
- `model.eval()` 모델링 시 training과 inference시에 다르게 동작하는 layer들이 존재한다. 예를 들면, Dropout layer는 학습시에는 동작해야하지만, inference시에는 동작하지 않는 것과 같은 예시를 들 수 있다. model.eval()는 이런 layer들의 동작을 inference(eval) mode로 바꿔준다는 목적으로 사용된다. 


### block을 쌓기 위한 Module  
- `nn.Sequential` 여러 nn.Module을 한 컨테이너에 넣고 한번에 돌리는 방법. 컨테이너에 적힌 순서대로 값을 전달해 처리. 빠르고 간단히 사용하기 편함
- `nn.ModuleList` 각 Layer를 리스트에 전달하고 레이어의 iterator를 만듬. forward 파트를 간단하게 작성 가능  

```python
class MyModule(nn.Module):
    def __init__(self):
        super(MyModule, self).__init__()
        self.linears = nn.ModuleList([nn.Linear(10, 10) for i in range(10)])

    def forward(self, x):
        # ModuleList can act as an iterable, or be indexed using ints
        for i, l in enumerate(self.linears):
            x = self.linears[i // 2](x) + l(x)
        return x  
```

### 벡터 Embedding  
- `nn.Embedding()` 특정 단어와 맵핑되는 정수를 인덱스로 가지는 임베딩 벡터 테이블을 만듬. 기본적으로 num_embeddings과 embedding_dim을 인자로 받음

```python
# 데이터 전처리
train_data = 'you need to know how to code'
word_set = set(train_data.split()) # 중복을 제거한 단어들의 집합인 단어 집합 생성.
vocab = {tkn: i+2 for i, tkn in enumerate(word_set)}  # 단어 집합의 각 단어에 고유한 정수 맵핑.
vocab['<unk>'] = 0
vocab['<pad>'] = 1
```  
  
```python
import torch.nn as nn
embedding_layer = nn.Embedding(num_embeddings = len(vocab), 
                               embedding_dim = 3,
                               padding_idx = 1)
                               
print(embedding_layer.weight)
Parameter containing:
tensor([[-0.1778, -1.9974, -1.2478],
        [ 0.0000,  0.0000,  0.0000],
        [ 1.0921,  0.0416, -0.7896],
        [ 0.0960, -0.6029,  0.3721],
        [ 0.2780, -0.4300, -1.9770],
        [ 0.0727,  0.5782, -3.2617],
        [-0.0173, -0.7092,  0.9121],
        [-0.4817, -1.1222,  2.2774]], requires_grad=True)
```

### Tensor Copy
- `torch.clone()` 원본 input과 동일한 저장이 필요한 경우, clone()을 이용하여 복사할 수 있다. 복사시 자동 미분도 뒤따라옴으로 backprop을 원치 않을시 detach를 해줘야 한다  

```python
>>> t = torch.rand(1, requires_grad=True)
>>> t.clone()
tensor([0.4847], grad_fn=<CloneBackward>) # <=== as you can see here

>>> t = torch.rand(1, requires_grad=True)
>>> t.detach().clone()
tensor([0.4847])
```

### Tensor 차원 변경
- `torch.permute()` transpose는 2개의 차원만 교환할 수 있는 반면, permute는 모든 차원을 교환할 수 있다.  
```python
x = torch.rand(16,32,3)
y = x.transpose(0,2) #[3,32,16]
z = x.permute(2,1,0) #[3,32,16]
```


- `torch.repeat()` 특정 텐서의 sizes 차원의 데이터를 반복. 1D Tensor의 경우, [n]이 아닌 [1,n]으로 간주한다.
```python
>>> x = torch.tensor([1, 2, 3])     # 차원 [3] -> [1,3]
>>> x.repeat(4, 2)
tensor([[ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3]])  # 차원 [4,6]으로 바뀜
>>> x.repeat(4, 2, 1).size()
torch.Size([4, 2, 3])
```

## 자주사용하는 함수
- `summary()` Pytorch 모델을 Summary해주는 Torch Summary Module.

```python
from torchsummary import summary
summary(model(), input_size=(3,size,size), device='cpu')
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
**[4] [no_grad()와 eval()의 차이](https://coffeedjimmy.github.io/pytorch/2019/11/05/pytorch_nograd_vs_train_eval/)**  
**[5] [Python argparse 사용법](https://greeksharifa.github.io/references/2019/02/12/argparse-usage/)**  


