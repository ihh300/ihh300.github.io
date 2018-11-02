---
title: Photography
layout: single
permalink: /photography/
header:
  image: assets/images/banner/ihh330-post.jpg
  caption: "Data science ©ihh300"
classes: wide

---
My photography gallery of pictures taken in Canada, France and United Kingdom.

<table>
{% tablerow photography in site.photography %}
  {{ photography.title }}
{% endtablerow %}
</table>


{% for photography in site.photography %}
<a href="{{ photography.url | prepend: site.baseurl }}">
        <h2>{{ photography.title }}</h2>
</a>
{% endfor %}      


