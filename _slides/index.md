---
layout: page
title: Slides
excerpt: "Slides"
search_omit: true
---

<ul class="post-list">
{% for file in site.collections.slides.files %}
  <li><a href="{{ site.url }}{{ file.url }}">{{ file.url }}"</a></li>
{% endfor %}
</ul>
