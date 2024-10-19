---
layout: page
title: Categories
permalink: /categories/
---

{% for category in site.categories %}
  <h3 id="{{ category[0] | slugize }}">{{ category[0] }}</h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}