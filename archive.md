---
layout: page
title: Archive
permalink: /archive/
---


  {% for post in site.posts %}
    {% assign currentdate = post.date | date: "%Y" %}
    {% if currentdate != date %}
      {% if date != nil and forloop.index != 1 %}{% endif %}
      {{ currentdate }}
      
      {% assign date = currentdate %}
    {% endif %}
    {{ post.title }}
    {% if forloop.last %}<% endif %}
  {% endfor %}
  
  {% if date != nil and forloop.last %}<% endif %}