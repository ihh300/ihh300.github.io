---
layout: archive
author_profile: true
excerpt: "Blog on data science, data analysis and visualization"
---

This is the homepage and blog of Isabelle H, Data Scientist. 
For more about me, <a href="/about/" style="text-decoration: underline">see here</a>.

Recent posts
====================

{% for post in paginator.posts %}
  {% include archive-single.html %}
{% endfor %}

{% include paginator.html %}
