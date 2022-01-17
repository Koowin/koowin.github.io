---
title: "운동"
layout: archive
permalink: categories/workout
sidebar_main: true
---

{% assign posts = site.categories.workout %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}