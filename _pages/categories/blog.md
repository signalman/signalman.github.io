---
title: "Blog"
layout: category
permalink: /categories/blog/
sidebar:
  nav: "categories"
---
{% assign posts = site.categories.blog %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
