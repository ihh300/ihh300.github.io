---
layout: archive
title: "Portfolio"
permalink: /archive/
header:
  image: assets/images/banner/ihh330-half.jpg
  caption: "Data science ©ihh300"
classes: wide
---
Machine Learning is a field of artificial intelligence dedicated to build algorithms and models, supervised or unsupervised, so to infer, predict and answer specific busines or societal questions. I blog about my projects to document my portfolio.


{% for post in site.posts %}
  * [ {{ post.title }} ]({{ post.url }})
{% endfor %}
