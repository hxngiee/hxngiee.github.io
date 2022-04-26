---
layout: post
title: Instance-aware Image-to-Image Translation
subtitle: Utilizing the set structured side information  
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
