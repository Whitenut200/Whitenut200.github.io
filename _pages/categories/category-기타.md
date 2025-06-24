---
title: "기타"
layout: archive
permalink: categories/기타
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Tableau']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}