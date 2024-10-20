---
layout: page
title: Archive
permalink: /archive/
---


{% assign current_year = nil %}

{% for post in site.posts %}
  {% assign post_year = post.date | date: "%Y" %}
  
  {% if post_year != current_year %}
    {% if current_year != nil %}{% endif %}
    {{ post_year }}
    
    {% assign current_year = post_year %}
  {% endif %}
  
  {{ post.title }}
  
  {% if forloop.last and current_year == post_year %}{% endif %}
{% endfor %}
{% if current_year != nil and forloop.last and current_year != site.posts.first.date | date: "%Y" %}{% endif %}