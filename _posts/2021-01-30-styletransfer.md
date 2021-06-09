---
layout: post
title: StyleTransfer Experiment - 작성중
subtitle: Styling 효과를 결정짓는 Reference Image Size와 Network의 Receptive Fields
thumbnail-img: /assets/img/styletransfer_1.jpg
share-img: /assets/img/styletransfer_1.jpg
tags: [Experiment]
comments: true
---

## Table of contents
- [Problem Definition](#problem-definition)
- [Reference Image와 StyleTransfer간의 관계](#reference-image와-styletransfer간의-관계)
- [Styling 효과를 결정짓는 Image Size와 Network의 Receptive Fields](#styling-효과를-결정짓는-image-size와-network의-receptive-fields)
- [마치며](#마치며)  
  
## Problem Definition

<center>
<img src="/assets/img/styletransfer_5.png" alt="Component model visualisation">
</center>  
<em> Style Transfer시 단색 필터를 적용한 것과 같은 효과를 얻은 예시 사진 </em>

과제 마일스톤으로 StyleTransfer 네트워크를 학습하는도중, 참조 이미지의 특성에 따라 Styling 결과가 달리 나오는 것을 발견했습니다. 네트워크 파라미터를 동일한 값으로 설정했을 때, 어떤 참조 이미지의 경우 원본 이미지에 전반적인 비주얼 컨셉을 담아내는 반면, 다른 참조 이미지의 경우 단색 필터를 적용한 것과 같은 효과를 얻었습니다. 실험을 거듭하며, 참조 이미지의 Shape 왜곡 정도, 색깔과 질감의 다양성에 따라 Styling 결과가 다르게 나타난다는 것을 발견했습니다.


## Reference Image와 StyleTransfer간의 관계  
> Reference Image의 특성을 어떻게 적절히 반영할 수 있을까?  

<center>
<img src="/assets/img/styletransfer_4.jpg" alt="Component model visualisation">
<br>
<em> Low Level의 Layer일수록 참조 이미지의 작은 패턴을, High Level의 Layer일수록 전체적인 느낌을 담아낸다 </em>
</center>  

하나의 네트워크가 다양한 참조 이미지의 비주얼 특성을 반영하지 못한 이유는 다음과 같습니다. 참조 이미지의 경우 이미지에 따라 가지는 style 복잡도가 다른데, 네트워크는 학습시 고정된 content/style weight 비율로 학습되다보니 참조 이미지의 다양성을 모두 커버하지 못하는 것입니다. 또한 Inference시에도 특정 Layer를 기준으로 이미지를 Reconstruction하다보니 이미지에 특성에 따라 Styling의 효과가 다르게 나타납니다. 따라서 참조 이미지의 표현된 스타일의 정량값에 따라 적정 Layer를 선택하는 전략이 필요합니다 

## Styling 효과를 결정짓는 Image Size와 Network의 Receptive Fields  

<center>
<img src="/assets/img/styletransfer_1.jpg" alt="Component model visualisation">
<br>
<p style="width:50%;height:400px;float:left;overflow:hidden;">
<img alt="1" src="/assets/img/styletransfer_2.jpg"  style="height:100%;"/>
</p>
<p style="width:50%;height:400px;overflow:hidden;">
<img alt="2" src="/assets/img/styletransfer_3.jpg"  style="height:100%;"/>
</p>
<em> Left : trained with 160x160 style image / Right : trained with 960x960 style image</em>
</center>  

궁금증을 가지고 원인을 파악하던 중, Reference Image의 사이즈 조절로 다른 Styling 효과를 얻었다는 ISSUE를 읽었습니다. 위에 보이는 것과 같이 Image의 Size를 160x160으로 작게 줄여 학습시킬 경우, 네트워크가 참조 이미지의 local한 stroke feature에 주목하고, 960x960 이미지로 학습한 경우 참조 이미지의 global한 stroke feature에 주목하여 조금 더 단순한 이미지로 변환한 것이었습니다. 결과적으로 하나의 네트워크에서 Reference Image의 size와 네트워크의 receptive field가 어떻게 구성되었는지에 따라 Styling 효과가 다르게 나타나는 것을 알 수 있었습니다.

## 마치며
아직 시간적 여유가 없어 자세히 알아보진 못했지만, 실험을 마치고 몇가지 해결되지 않은 의문들이 있었습니다.  
1. Reference Image Size를 고정했을때 이미지의 특성에 상관없이 좋은 성능을 발휘하는 네트워크를 만들 수 있을까?
2. Receptive Fields의 크기가 고정되었을 때 작은 이미지의 경우 이미지의 더 많은 부분을 보고 큰 이미지의 경우 더 작은 부분을 보아서 반대의 결과가 나올 줄 알았다. 
3. 이미지에서 스타일의 복잡도는 어떻게 정량화할 수 있을까?(Edge의 개수?,Color의 다양성?)
4. Reference Image의 복잡도에 따라 Adaptive하게 Layer selection이나 이미지 resize를 해준다면?  


바쁜 일을 마무리하고 글을 다시 마무리하도록 하겠습니다

### Reference
**[1] [A Neural Algorithm of Artistic Style](https://arxiv.org/pdf/1508.06576.pdf)**  
**[2] [Neural STyle TF](https://github.com/cysmith/neural-style-tf)**  
**[3] [GITHUB ISSUE I](https://github.com/jcjohnson/fast-neural-style/issues/62)**  
**[4] [GITHUB ISSUE II](https://github.com/DmitryUlyanov/texture_nets/issues/47)**  
**[5] [Stroke Controllable Fast Style Transfer with Adaptive Receptive Fields](https://arxiv.org/abs/1802.07101)**  
