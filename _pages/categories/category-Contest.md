---
title: "Contest"
layout: archive
permalink: Project/Contest
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['Contest']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
