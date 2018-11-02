---
title: Photography
layout: single
permalink: /portfolio/
classes: wide
---
My photography gallery of pictures taken in Canada, France and United Kingdom.

{% for photography in site.photography %}
  <a href="{{ photography.url }}">
    <h2>{{ photography.title }}</h2>
  </a>
{% endfor %}
