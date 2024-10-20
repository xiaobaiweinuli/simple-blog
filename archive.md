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

<li>
<a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
{% if current_year != nil %}{% endif %}