---
layout: post
title: ML Concepts
subtitle: 기본 용어의 개념과 자주 사용하는 기법 정리
tags: [ML, Pytorch]
use_math: true
comments: true
---

## Table of contents
- [기본 용어의 개념](#기본-용어의-개념)
- [자주 사용하는 기법](#자주-사용하는-기법)

## 기본 용어의 개념

### Inductive bias  
### GAN Evaluation Metric  
- LPIPS: Learned Perceptual Image Patch Similarity
    - 두 이미지의 perceptual distance를 계산하는 방식
- FID: Fréchet Inception Distance
    - $FID={\parallel\mu_x-\mu_y\parallel}^2 -Tr(\sum_x + \sum_y -2\sum_x\sum_y)$
    - 실제 training dataset의 distribution과 생성된 영상의 distribution의 거리를 계산하는 방식
    - Inception network의 중간 레이어에서 feature를 가져와, 실제 데이터와 생성된 데이터에서 얻은 feature의 평균과 공분산을 비교하는 식으로 구성
    - Random Generation 성능 평가시 사용, FID가 낮을수록 좋은 성능

### seamless  
- 뛰어난 호환성, 부드러운 상호연결성
- 소프트웨어분야에서 여러개의 프로그램이 마치 원래 하나였던 것처럼 깔끔한 인터페이스로 연결되어 있는 것을 뜻함
- transformer가 여러 도메인(영상, 음성 등)의 task를 잘 처리하는 특징을 seamless하다고 표현


## 자주 사용하는 기법  
### Global Average Pooling
- CNN + FC Layer에서 classifier인 FC Layer를 없애기 위한 방법으로 도입
- 어떤 크기의 feature라도 같은 채널의 값들을 하나의 평균 값으로 대체 (H,W,C) -> (1,1,C)
- 파라미터가 추가되지 않아 연산 측면에서 유리하고 over fitting도 완화할 수 있음
- FC Layer는 파라미터수가 과도하게 증가하는 단점이 있으며 overffint 유발



### Reference
**[1] [Global Average Pooling 이란](https://gaussian37.github.io/dl-concept-global_average_pooling/)**  
**[2] [Inception Score & Frechet Inception Distance](https://cyc1am3n.github.io/2020/03/01/is_fid.html)**  
