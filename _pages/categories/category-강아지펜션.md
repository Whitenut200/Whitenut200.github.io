---
title: "개인프로젝트"
layout: archive
permalink: categories/개인프로젝트
author_profile: true
sidebar_main: true
types: posts
---

{% assign posts = site.categories['개인프로젝트']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}