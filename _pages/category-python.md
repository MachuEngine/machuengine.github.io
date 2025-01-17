---
title: "python"
layout: archive
permalink: /python
---
{% assign posts = site.categories.python %}
{% for post in posts %}
  {% include archive-single.html type="entries" %}
{% endfor %}
