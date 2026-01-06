---
title: "Marketing"
layout: archive
permalink: Project/Marketing
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Marketing']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}