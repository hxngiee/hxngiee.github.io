---
layout: post
title: Beautiful-jekyll post template
tags: [homepage]
comments: true
---

# Beautiful Jekyll
> *Copyright 2016 [Dean Attali](http://deanattali.com). Licensed under the MIT license.*

**Beautiful Jekyll** is a ready-to-use template to help you create an awesome website quickly. Perfect for personal blogs or simple project websites.

### Table of contents
- [Prerequisites](#prerequisites)
- [Build your website in 3 steps](#build-your-website-in-3-steps)

## Prerequisites
- You need to have a GitHub account. If you don't have one, [sign up here](https://github.com/join) - it takes one minute. This is where your website will live - if you sign up with username `johnsmith` then your website will be `http://johnsmith.github.io`.  

#### Personal websites 
| Website | Who | What |
| :------ |:--- | :--- |
| [deanattali.com](http://deanattali.com) | Dean Attali | Creator of Beautiful Jekyll |
| [ouzor.github.io](http://ouzor.github.io) | Juuso Parkkinen | Data scientist |
| [derekogle.com](http://derekogle.com/) | Derek Ogle | Professor of Mathematical Sciences and Natural Resources |
| [trappmartin.github.io](http://trappmartin.github.io) | Martin Trapp | Machine learning researcher |

### Very advanced: Local development
Beautiful Jekyll is meant to be so simple to use that you can do it all within the browser. However, if you'd like to develop locally on your own machine, that's possible too if you're comfortable with command line. Follow these simple steps to do that with Vagrant:

1. Install [VirtualBox](http://virtualbox.org) and [Vagrant](https://www.vagrantup.com)
2. Clone your fork `git clone git@github.com:yourusername/yourusername.github.io.git`
3. Inside your repository folder, run `vagrant up`

Disclaimer: I personally am NOT using local development so I don't know much about running Jekyll locally. If you follow this route, please don't ask me questions because unfortunately I honestly won't be able to help!

### Credits
This template was not made entirely from scratch. I would like to give special thanks to:
- [Barry Clark](https://github.com/barryclark) and his project [Jekyll Now](https://github.com/barryclark/jekyll-now)

### Contributions
Thank you to [all contributors](https://github.com/daattali/beautiful-jekyll/graphs/contributors). Special thanks to the following people with non-trivial contributions (in chronological order): [@hristoyankov](https://github.com/hristoyankov), [@jamesonzimmer](https://github.com/jamesonzimmer), [@XNerv](https://github.com/XNerv), [@epwalsh](https://github.com/epwalsh), [@rtlee9](https://github.com/rtlee9).

#### 이미지 가운데 정렬
<center>
<img src="/assets/img/avatar-icon.png" alt="Component model visualisation">
<br>
<em>An <a href="https://github.com/ouzor/eyediagram">"Eye Diagram"</a> 주석 </em>
</center>

#### Code Block
{% highlight python %}
# simple weighting, importance: num_my_tiles > num_enemy_tiles > enemies_dist
return sum([num_my_tiles * 10000000, num_enemy_tiles * -100000, enemies_dist])
{% endhighlight python %}

### Reference
[Beautiful-jekyll 전반적인 기능](https://dymaxionkim.github.io/beautiful-jekyll/2017-01-10-make-blog/) 




