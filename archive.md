---
layout: page
title: Archive
permalink: /archive/
---

{% assign date = "0000" %} <!-- 初始化date变量为一个不可能的年份 -->

{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h1 id="y{{post.date | date: "%Y"}}">{{ currentdate }}</h1>
    <ul>
    {% assign date = currentdate %}
  {% endif %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}

<!-- 如果循环结束时<ul>标签没有关闭，添加一个检查 -->
{% unless forloop.last %}</ul>{% endunless %}