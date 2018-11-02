---
title: Photography
layout: collection
collection: portfolio
permalink: /portfolio/
entries_layout: list
show_excerpts: false
sort_by: title
sort_order: forward
classes: wide
---
My photography gallery of pictures taken in Canada, France and United Kingdom.

{% for page in site.portfolio %}
  * {{ page.date | date_to_string }} &raquo; [ {{ page.title }} ]({{ page.url }})
{% endfor %}
