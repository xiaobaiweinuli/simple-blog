---
layout: page
title: Archive
permalink: /archive/
---


{% assign previous_date = nil %}
{% for post in site.posts %}
  {% assign current_date = post.date | date: "%Y-%m-%d" %}
  {% if current_date != previous_date %}
    {% if previous_date != nil %}{% endif %}
    {{ current_date }}
    
  {% endif %}
<li>
<a href="/blog/{{ post.url }}">{{ post.title }}</a></li>
  {% assign previous_date = current_date %}
{% endfor %}
{% if previous_date != nil %}{% endif %}