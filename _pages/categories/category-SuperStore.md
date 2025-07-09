---
title: "SuperStore"
layout: archive
permalink: categories/SuperStore
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['SuperStore']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}