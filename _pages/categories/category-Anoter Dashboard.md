---
title: "Another Dashboard"
layout: archive
permalink: Project/Another Dashboard
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Another Dashboard']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}