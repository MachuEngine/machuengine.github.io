---
title: "it"
layout: archive
permalink: /it
---
{% assign posts = site.categories.it %}
{% for post in posts %}
  {% include archive-single.html type="entries" %}
{% endfor %}
