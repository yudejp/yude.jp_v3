---
layout: default
title: 📕 ブログ
permalink: /blog/
---
{% assign counter = 0 %}
{% for post in site.posts %}
  {% assign counter = counter | plus: 1 %}
{% endfor %}
{%- assign date_format = site.minima.date_format | default: "%Y/%-m/%-d" -%}

<p><span style="font-size: 2rem">{{counter}}</span> 件の記事があります。</p>
<ul>
  {% for post in site.posts %}
    <li>
      <p><a href="{{ post.url }}">{{ post.title }}</a></p>
      <p style="margin-top: -14px">
      {% if post.tags.size > 0 %}
      <i class="fa-solid fa-tags"></i>
      {% endif %}
      {% for tag in post.tags %}
      <span class="badge rounded-pill bg-success">{{ tag }}</span>
      {% endfor %}
      <i style="margin-left: 3px"
                class="fa-solid fa-calendar-days"></i>
      {{ post.date | date: date_format }}
      </p>
    </li>
  {% endfor %}
</ul>