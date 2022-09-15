---
title: "Project"
layout: category
permalink: /categories/project/
sidebar:
  nav: "categories"
---
{% assign posts = site.categories.project %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
