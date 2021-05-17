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
정규화 기법을 이해하기 위한 사전 지식으로 Feature Block에 대해 설명합니다. 고양이 이미지가 하나의 Layer를 통과할 때, 6개 Feature를 얻었다고 가정합니다. 각 채널별 Feature 이미지를 1D-array로 Flatten시켜 6개의 1D-Array를 갖습니다. 여기서 하나의 열은 해당 채널의 Feature 이미지를, 행은 Feature 이미지별 같은 Position을 나타냅니다. 채널별 Feature Array를 모아 Matrix로 바꾸고 이를 Batch 단위로 쌓아 최종 Feature Block을 만듭니다. 

### Normalization Variants
<center>
<img src="/assets/img/pono-normalization_variants.png" alt="Component model visualisation">
</center>  
이미지 생성 분야에서 Instance Normalization은 이미지별 feature statistics를 직접 normalize함으로써 style variation을 제거하는 효과를 가져오고 Style Transfer 분야에서 Batch Normalization을 대체하는 모듈로 활발히 활용되어왔습니다(BN의 경우 배치단위로 normalize가 이뤄지기 때문에 domain별 스타일이 뭉뚱그려져 학습되는 문제가 있었습니다, IN은 이미지 하나 하나를 쪼개서 normalize하여 stylie 학습에 잘 작동한다고 알려져 있습니다. )

## Positional Normalization
<center>
<img src="/assets/img/pono-moments.png" alt="Component model visualisation">
</center>  
Positional Normalization 적용시 네트워크가 성공적으로 이미지(고양이, 모나리자)의 General한 Structure를 포착한 것을 확인할 수 있습니다. 특히 초기 layer에서는 눈과 귀같은 이미지의 details한 부분들을 포착해내고, 후기 layer에서는 전반적인 shape를 포착한 것을 알 수 있습니다.


<center>
<img src="/assets/img/pono-pono_ms.png" alt="Component model visualisation">
</center>  
기존 Normalization Method의 경우 Encoding 단계에서 구한 Feature Statistics이 사용되고 버려지나, Positional Normalization에서는 해당 정보를 Decoding시 다시 활용하여 GAN이 Structural한 정보를 더 쉽게 복원하도록 돕습니다.

## Experiments and Analysis
- 

## Conclusion
- 
