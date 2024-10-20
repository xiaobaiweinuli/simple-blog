---
layout: page
title: Archive
permalink: /archive/
---


{% assign previous_year = nil %}
{% for post in site.posts %}
  {% assign current_year = post.date | date: "%Y" %}
  {% if current_year != previous_year %}
    {% if previous_year != nil %}{% endif %}
    {{ current_year }}
    
  {% endif %}
  {{ post.title }}
  {% assign previous_year = current_year %}
{% endfor %}
{% if previous_year != nil %}{% endif %}