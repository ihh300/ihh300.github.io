---
title: Photography
layout: single
permalink: /portfolio/
classes: wide
---
My photography gallery of pictures taken in Canada, France and United Kingdom.

<ul>
  {% for portfolio in site.portfolio %}
    <li>
      <a href="{{ portfolio.url }}">{{ portfolio.title }}</a>
      - {{ portfolio.headline }}
    </li>
  {% endfor %}
</ul>
