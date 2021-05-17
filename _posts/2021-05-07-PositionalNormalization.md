---
layout: post
title: Positional Normalization - 작성중 
subtitle: Keeps position and Normalize across channel
thumbnail-img: /assets/img/pr_pono.png 
tags: [Paper Review]
comments: true
---

## Table of contents
- [Abstract](#abstract)
- [Normalization Method](#normalization-method)
- [Positional Normalization](#positional-normalization)
- [Experiments and Analysis](#experiments-and-analysis)
- [Conclusion](#conclusion)  


## Abstract
- NIPS'19 spotlight에 발표된 Normalization 기법
- Pixel position별 Feature 차원의 정규화를 통해, 네트워크가 Structural한 정보를 쉽게 파악하도록 도움
- GAN에 적용하였을 때, baseline 모델 성능이 크게 향상되는 것을 보임


## Normalization Method
### Feature Block
<center>
<img src="/assets/img/pono-deepfeature.png" alt="Component model visualisation">
</center>  
정규화 기법을 이해하기 위한 사전 지식으로 Feature Block에 대해 설명합니다. 고양이 이미지가 하나의 Layer를 통과할 때, 6개 feature를 얻었다고 가정합니다. 각 채널별 feature 이미지를 1d array로 flatten시켜 6개의 1d array를 갖습니다. 여기서 하나의 열은 해당 채널의 Feature 이미지를, 행은 Feature 이미지별 같은 position을 나타냅니다. 채널별 feature array를 모아 Matrix로 바꾸고 이를 batch 단위로 쌓아 최종 Feature Block을 만듭니다. 

### Normalization Variants
<center>
<img src="/assets/img/pono-normalization_variants.png" alt="Component model visualisation">
</center>  

- 

## Positional Normalization

<center>
<img src="/assets/img/pono-moments.png" alt="Component model visualisation">
</center>  

<center>
<img src="/assets/img/pono-pono_ms.png" alt="Component model visualisation">
</center>  
기존 Normalization Method의 경우 Encoding 단계에서 구한 통계값을 Vanish Gradient를 완화할 목적으로 사용되고 버려지나, Positional Normalization에서는 해당 정보를 Decoding시 다시 활용하여 GAN이 Structural한 정보를 더 쉽게 복원하도록 돕습니다.

## Experiments and Analysis
- 

## Conclusion
- 
