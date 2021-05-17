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
<center>
<p style="width:50%;height:400px;float:left;overflow:hidden;">
<img alt="1" src="/assets/img/pono-deepfeature.jpg"  style="height:100%;"/>
</p>
<p style="width:50%;height:400px;overflow:hidden;">
<img alt="2" src="/assets/img/pono-normalization_variants.png"  style="height:100%;"/>
</p>
<em> Left : AFHQ 고양이 이미지 / Right : 일반 이미지에 Canny를 적용한 이미지</em>
</center> 

<center>
<img src="/assets/img/pono-deepfeature.png" alt="Component model visualisation">
</center>  
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

- 

## Experiments and Analysis
- 

## Conclusion
- 
