---
layout: post
title: Project - Sketch2Art  
subtitle: Creating Artistic Images from Freehand Sketches 
thumbnail-img: /assets/img/projects_sketch2art.png 
tags: [Project, Image-to-Image Translation]
comments: true
---

{: .box-note}
**진행기간:** 2021.03 ~ 진행 중  
**Team:** 김기홍, 김정윤, 이건호  
**주요내용:** 소통 약자의 감정 표현과 창작 의도를 용이하게 전달해주는 자동 스케치 채색 및 스타일링 툴 개발  
**기여한 점:** Unsupervised Image-to-Image Translation Model에 Positional Normalization 적용하여 baseline 모델 성능 향상, Input 이미지의 Content 보존을 위한 Masking Module 적용, Flask를 이용한 Pytorch 모델 배포  
**사용한 Skill 또는 지식:** Pytorch, Flask, Unsupervised Image-to-Image Translation  


## Table of contents
- [Introduction](#introduction)
- [Data Processing](#data-processing)
- [Reference Image와 StyleTransfer간의 관계](#reference-image와-styletransfer간의-관계)
- [Styling 효과를 결정짓는 Image Size와 Network의 Receptive Fields](#styling-효과를-결정짓는-image-size와-network의-receptive-fields)
- [마치며](#마치며)  


## Introduction
글.  


## Data Processing
- Sketch Data는 Object의 Edge를 바탕으로 구성된 흑백 이미지로 딥러닝 학습에 필요한 데이터의 양이 충분치 않음
- 일반적으로 많이 알려진 pix2pix의 edges2shoes, edges2handbags의 경우, 다수의 dataset(5만개, 13만개)가 존재하나 새로운 카테고리에 대한 Sketch를 구하고자 할 경우, 해당 카테고리에 대한 Edge Detection과 Post-Processing 작업이 필요
- 본 글에서는 Semantic Segmentation 네트워크(DeepLabv3 사용)를 이용하여 일반 사진으로부터 특정 class에 대한 이미지를 검출/가공하고 해당 이미지를 딥러닝 학습에 적용하기 위한 절차를 서술

1. Object Define
2. Crop for easy training 
3. Using Segmented Image as mask using deeplab3
4. background reverse
5. Guassian blur -> blur, Aperature
6. 공백 이미지 제거


<center>
<img src="/assets/img/styletransfer_5.png" alt="Component model visualisation">
</center>  

글.
