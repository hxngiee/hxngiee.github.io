---
layout: post
title: StyleTransfer와 실험기
subtitle: Styling 효과를 결정짓는 Reference Image Size와 Network의 Receptive Fields
tags: [실험일지]
comments: true
---

## Table of contents
- [문제인식](#문제인식)
- [Reference Image와 StyleTransfer간의 관계](#reference-image와-styletransfer간의-관계)
- [Styling 효과를 결정짓는 Image Size와 Network의 Receptive Fields](#styling-효과를-결정짓는-image-size와-network의-receptive-fields)
- [마치며](#마치며)
  

## 문제인식

<center>
<img src="/assets/img/avatar-icon.png" alt="Component model visualisation">
<br>
<em>An <a href="https://github.com/ouzor/eyediagram">"Page Link"</a> 주석 </em>
</center>  

과제 마일스톤으로 StyleTransfer 네트워크를 학습하는도중, 참조 이미지의 특성에 따라 Styling 결과가 달리 나오는 것을 발견했다. 네트워크 파라미터를 동일한 값으로 설정했을 때, 어떤 참조 이미지의 경우 원본 이미지에 전반적인 비주얼 컨셉을 담아내는 반면, 다른 참조 이미지의 경우 단색 필터를 적용한 것과 같은 효과를 얻었다. 실험을 거듭하며, 참조 이미지의 Shape 왜곡 정도, 색깔과 질감의 다양성에 따라 Styling 결과가 다르게 나타난다는 것을 발견했다.


## Reference Image와 StyleTransfer간의 관계  
> Reference Image의 특성을 어떻게 적절히 반영할 수 있을까?  

하나의 네트워크가 다양한 참조 이미지의 비주얼 특성을 반영하지 못한 이유는 다음과 같다. 참조 이미지의 경우 이미지에 따라 가지는 style 복잡도가 다른데, 네트워크는 학습시 고정된 content/style weight 비율로 학습되다보니 참조 이미지의 다양성을 모두 커버하지 못하는 것이다. 또한 Inference시에도 특정 Layer를 기준으로 이미지를 Reconstruction하다보니 이미지에 특성에 따라 Styling의 효과가 다르게 나타난다. 따라서 참조 이미지의 표현된 스타일의 정량값에 따라 적정 Layer를 선택하는 전략이 필요하다 

## Styling 효과를 결정짓는 Image Size와 Network의 Receptive Fields  
궁금증을 가지고 원인을 파악하던 중, Reference Image의 사이즈 조절로 다른 Styling 효과를 얻었다는 ISSUE를 읽었다. 위에 보이는 것과 같이 Image의 Size를 160x160으로 작게 줄여 학습시킬 경우, 네트워크가 참조 이미지의 local한 stroke feature에 주목하고, 960x960 이미지로 학습한 경우 참조 이미지의 global한 stroke feature에 주목하여 조금 더 단순한 이미지로 변환한 것이다. 결과적으로 하나의 네트워크에서 Reference Image의 size와 네트워크의 receptive field가 어떻게 구성되었는지에 따라 Styling 효과가 다르게 나타나는 것을 알 수 있었다.

## 마치며
실험을 마치며 몇가지 해결되지 않은 의문들이 있었다.  
1. Reference Image Size를 고정했을때 이미지의 특성에 상관없이 좋은 성능을 발휘하는 네트워크를 만들 수 있을까?
2. Receptive Fields의 크기가 고정되었을 때 작은 이미지의 경우 이미지의 더 많은 부분을 보고 큰 이미지의 경우 더 작은 부분을 보아서 반대의 결과가 나올 줄 알았다. 
3. 이미지에서 스타일의 복잡도는 어떻게 정량화할 수 있을까?(Edge의 개수?,Color의 다양성?)
4. Reference Image의 복잡도에 따라 Adaptive하게 Layer selection이나 이미지 resize를 해준다면?  

아직 시간적 여유가 없어 자세히 알아보지 못하고 있다. 여바쁜 일을 마무리하고 못한 의문을 기록하며 글을 마무리한다.  

### Reference
**[1] [A Neural Algorithm of Artistic Style](https://arxiv.org/pdf/1508.06576.pdf)**  
**[2] [Neural STyle TF](https://github.com/cysmith/neural-style-tf)**  
**[3] [GITHUB ISSUE I](https://github.com/jcjohnson/fast-neural-style/issues/62)**  
**[4] [GITHUB ISSUE II](https://github.com/DmitryUlyanov/texture_nets/issues/47)**  
**[5] [Stroke Controllable Fast Style Transfer with Adaptive Receptive Fields](https://arxiv.org/abs/1802.07101)**  