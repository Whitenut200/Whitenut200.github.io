---
title: "Project"
layout: archive
permalink: /Project/
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Project']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}