---
layout: post
title: Project - Sketch2Art  
subtitle: Creating Artistic Images from Freehand Sketches 
thumbnail-img: /assets/img/projects_sketch2art.png 
tags: [Project, Image-to-Image Translation]
comments: true
---

{: .box-note}
**진행기간:** 2020.03 ~ 진행 중  
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

<center>
<img src="/assets/img/styletransfer_5.png" alt="Component model visualisation">
</center>  

글.