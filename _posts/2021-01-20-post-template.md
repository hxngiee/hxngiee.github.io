---
layout: post
title: Beautiful-jekyll Post Template
subtitle: Excerpt from Soulshaping by Jeff Brown
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [homepage]
comments: true
---

# Beautiful Jekyll
> *Copyright 2016 [Dean Attali](http://deanattali.com). Licensed under the MIT license.*  

Beautiful Jekyll **볼드체** is a ready-to-use template

## Table of contents
- [Image Align](#image-align)
- [Text](#text)
- [Code Block](#code-block)
- [Table](#table)
  - [Block Boxing](#block-boxing)

> 제목 링크시 띄어쓰기는 `-`로 스펠링은 소문자로만 해야 먹음 

## Image Align
![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

<center>
<img src="/assets/img/avatar-icon.png" alt="Component model visualisation">
<br>
<em>An <a href="https://github.com/ouzor/eyediagram">"Eye Diagram"</a> 주석 </em>
</center>

## Text
1. Install [VirtualBox](http://virtualbox.org) and [@jamesonzimmer](https://github.com/jamesonzimmer).
2. Clone your fork `git`

- You need to have a `GitHub account`. If you don't have one, [sign up here](https://github.com/join) - it takes one minute.

## Code Block
```python
# simple weighting, importance: num_my_tiles > num_enemy_tiles > enemies_dist
return sum([num_my_tiles * 10000000, num_enemy_tiles * -100000, enemies_dist])
```

## Table

| First Header  | Second Header | Third Header         |
| :------------ | :-----------: | -------------------: |
| First row     | Data          | Very long data entry |
| Second row    | **Cell**      | *Cell*               |
| Third row     | Cell that spans across two columns  |123|

<center>
<em>An <a href="https://github.com/ouzor/eyediagram">"Eye Diagram"</a> 주석 </em>
</center>

## Block Boxing 

{: .box-note}
**Note:** This is a notification box.

{: .box-warning}
**Warning:** This is a warning box.

{: .box-error}
**Error:** This is an error box.


### Reference  
**[1] Beautiful-jekyll 전반적인 기능:** https://dymaxionkim.github.io/beautiful-jekyll/2017-01-10-make-blog/  
**[2] 마크다운(MARKDOWN) 문법 사용법:** https://eungbean.github.io/2018/06/11/How-to-use-markdown/
**[3] 홈페이지 더 빠르고 쉽게 편집하기:** http://prose.io/
