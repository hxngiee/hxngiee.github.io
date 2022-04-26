---
layout: post
title: Smooth Swap - A Simple Enhancement for Face-Swapping with Smoothness
subtitle: Focuses on deriving the smoothness of the identity embedding 
thumbnail-img: /assets/img/instagan_overview.jpg 
tags: [Paper Review]
use_math: true
comments: true
---
{: .box-note}
**FaceSwap:** Target이미지의 facial expressions, head pose, and backgrounds를 유지한채 Source 이미지의 persion-identity를 바꾸는 작업

## Table of contents
- [Abstract](#abstract)
- [Introduction](#introduction)
- [Problem Formulation](#problem-formulation)
- [Method](#smooth-swap)
- [Experiments](#experiments)
- [Evaluation Details](#evaluation-details)  
- [Conclusion](#conclusion)  


## Abstract  
- FaceSwap을 수행하기 위해  기존 방법론들의 경우 complex architectures와 loss functions을 설계하는 방식으로 디자인되어옴
    - 이러한 방식은 다양한 hyperparameter tuning이 요구되어 학습을 성공시키기까지 많은 수작업이 동반됨
    - 본 논문에서는 일일이 모델을 튜닝하는 방식 대신, 더욱 강건한 identity network(focus smoothness of the identity embedding)를 학습시켜 안정적인 face변환이 가능한 `Smooth-Swap` 방법론을 제안함

- FaceSwap을 어렵게 만드는 요인들(Assumption about difficulty of face-swapping)
    - non-smooth한 embedding space에서는 gradient가 unstable하게 optimize됨
    - 본 논문에서는 identity embedder를 `supervised contrastive learning` 방식으로 학습시켜 embedding space를 smooth하게 개선시킴
    - 비교 실험을 통해 smooth embedder가 더 빠르고 안정적이게 학습을 수렴시키고 가장 기본적인 아키텍쳐만으로도(simple U-Net based generator and three basic loss function) 기존 방법론보다 성능의 우위를 가지는 것을 보임


## Introduction
- FaceSwap시 faithful한 identity swapping을 위해선 얼굴의 shape을 변화시키는 것이 중요함
- 하지만 label(Swapped images)이 없는 Unsupervised Setting에서 guidance없이 pixel에 큰 변화를 주는 것은 어려운 일
- 이를 해결하기 위해 기존 방법론들의 경우, segmentation(mask-based mixing)이나 3DMM(3D face-shape modeling)과 같은 component를 추가하는 방식을 채택
- 이러한 방식은 face shape를 효과적으로 변화시키고 swapped 이미지의 퀄리티를 높일 수 있으나
- hyperparameter와 loss function에 의한 complexity가 증가하여 성공적인 학습이 더 어려워지는 문제가 있음
- 본 연구에서는, 개선된 smoothness를 가진 새로운 embedding model을 제안하여 외부 component를 의존하지 않고 효과적으로 대처할 수 있는 face-swapping 방법론을 제안함

**Contribution**  
Simple architecture
- simple U-Net based generator, which does not involve any handcrafted components as the existing models

Simple loss function
- using minimal loss(identity, pixel-level change, adv) function for face-swapping

Fast training
- smooth identity embedder allows faster training of the generator by providing more stable gradient information

## Problem Formulation
C1. Swapped된 이미지는 Source image의 identity를 가지고있어야한다
- $L(x_{swap}, x_{src})$

C2. Swapped된 이미지는 target image의 expression, pose and background를 유지해야한다
- $L(x_{swap}, x_{tgt})$  

- faceSwap 모델 학습의 어려움은 C1과 C2 사이의 상충관계로부터 비롯됨
    - C1을 강조하면 C2가 약해지고, C2를 강조하면 C1이 약해진다
- ($x_{swap}$과 $x_{tgt}$)간 loss를 걸어주며 ($x_{swap}$과 $x_{src}$)간 perceptual or pixel level loss를 걸어주어 Source의 특징을 반영하도록 함


## Method
### 3.1 Challenges for Changing Identity
- 위와 같은 loss를 통해 Source 이미지와 Target 이미지의 절충된 합성 이미지를 얻을 수 있음
- 사람을 identify하기 위해선 swapped face의 shape이 source shape에 맞게 적절히 바뀔 필요성이 있음
- 하지만 loss를 이용한 방법만으론 face shape(geometric transformation)을 변화시키기에 충분하지 않은 부분이 있음
- 기존 방법론(HifiFace)의 경우, face shape을 바꾸는데 3D Model을 활용하여 shape 정보를 포착하고 활용
- 본 논문에서는 추가적인 모델이나 데이터 없이 Identity Embedding Space를 견고하게 만드는 것만으로 face shape에 대한 변화를 더 잘 일으키는 것을 말하고 있음


### 3.2 Importance of A Smooth Identity Embedder (vs ArcFace)
- 대부분의 face swapping 모델들은 Arc-Face를 identity embedder로 활용하고 있음
    - 얼굴 이미지의 identitiy 유사도를 측정해주는 매트릭

- 하지만 기존 Arc-Face의 경우, 학습시 classification(discriminative한 task)을 기반으로 학습하기 때문에 embedding space가 매우 non-smooth하다는 단점이 있음
    - Arc-Face의경우, 사람들간의 차이가 크게 나는 특징을 위주로 학습하기 때문에 동일인물에 대한 변화(나이가 젊은, 나이든), (살이찐 , 다이어트한)에 대해선 구분하기 어려움
    - Smooth는 Contrastive loss를 통해 identity정보를 최대화하려는 방향으로 학습함으로써
        - positive sample을 비슷한 곳에 negative sample은 멀리 embedding
    - 이러한 풍부한 특징을 고려하여 구분할 수 있게끔 학습함

- $x_{swap}$을 생성해낼 때, gradient가 일관되고 정확해야 좋은 품질의 swapped 이미지를 얻을 수 있음
    - gradient는 generator가 이미지를 잘못합성하였을 때, 어떻게 수정되어야하는지 feedback을 줌
    - 모델이 identity vector에 따라 상반된 C1, C2 loss를 optimize하는데 합성된 이미지들이 급격히 변하면 최적의 합성 결과를 유도하기 어려움(loss surface가 불안정)

- non-smooth Embedding space의 경우, gradient direction이 noisy함
- smooth embedder의 경우 $x_{tgt}$의 identity를 변화시킬 때, 조금 더 smooth한 경로로 좋은 gradient direction을 제공
    - the ArcFace embedder보다 빠르고 안정적이게 학습을 돕는 것을 보임

## Method: Smooth-Swap
