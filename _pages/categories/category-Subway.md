---
title: "Subway"
layout: archive
permalink: Project/Subway
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Subway']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}