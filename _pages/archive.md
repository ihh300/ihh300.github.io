---
layout: archive
title: "Posts"
permalink: /archive/
header:
  image: assets/images/banner/ihh330-half.jpg
  caption: "Data science ©ihh300"
classes: wide
---
{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
