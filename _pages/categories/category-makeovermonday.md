---
title: "Makeovermonday"
layout: archive
permalink: Project/Makeovermonday
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Makeovermonday']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}