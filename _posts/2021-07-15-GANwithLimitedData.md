---
layout: post
title: Training Generative Adversarial Networks with Limited Data - 작성중
subtitle: Adaptive discriminator augmentation that significantly stabilizes training in limited data
thumbnail-img: /assets/img/GANwithLimitedData-flowchart.jpg
tags: [Paper Review]
use_math: true
comments: true
---

## Table of contents
- [Abstract](#abstract)  
- [Introduction](#introduction)  

## Abstract
- Data-driven 모델인 StyleGAN2는 학습시 약 7만장 이상의 고해상도 이미지가 요구된다. 하지만 학습에 필요한 다수의 고해상도 이미지를 구하는 것은 현실적으로 많은 어려움이 뒤따른다.
- 저자는 적은 데이터로 높은 학습 안정성을 제공하는 Adaptive Discriminator Augmentation을 제안하여 데이터가 제한된 상황에서도 높은 Visual Qulity를 확보할 수 있는 Mechanism을 제시했다.
- 기존 모델에 Adaptive Discriminator Augmentation을 추가한 실험에서 SOTA급 성능을 보여주며 생성 모델이 다양한 Domain에서 활용될 수 있는 가능성을 보여줬다.

## Introduction
- introduce a concept of using zero shot in computer vision
