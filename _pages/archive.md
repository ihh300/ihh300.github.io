---
layout: archive
title: "Portfolio"
permalink: /archive/
header:
  image: assets/images/banner/ihh330-half.jpg
  caption: "Data science ©ihh300"
classes: wide
---
Machine Learning is a field of artificial intelligence that studies the methods of building models that can be trained, as well as algorithms for their construction and learning. I blog about my projects to document my portfolio.


{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
