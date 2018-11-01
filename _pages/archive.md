---
layout: archive
title: "Posts"
permalink: /archive/
header:
  image: assets/images/banner/banner_toronto.jpg
  caption: "Toronto"
author_profile: false
---

## Blog Posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
