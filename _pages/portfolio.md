---
title: Photography
layout: archive
permalink: /portfolio/
classes: wide
---
My photography gallery of pictures taken in Canada, France and United Kingdom.

{% for page in site.portfolio %}
  * {{ page.date | date_to_string }} &raquo; [ {{ page.title }} ]({{ page.url }})
{% endfor %}
