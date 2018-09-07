---
layout: page
title: 分类
menu: true
order: 2
description: >
  这里包含了所有的文章列表
accent_color: rgb(38,139,210)
accent_image:
  background: rgb(32,32,32)
  overlay:    false
---

{% for category in site.categories %}<a class="button" href="#{{ category | first }}">{{ category | first }}</a> {% endfor %}

{% for category in site.categories %}
<h2><a id="{{ category | first }}">{{ category | first }}</a></h2>

<ul class="title-list">
{% for post in category.last %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}<span>{{ post.date | date:"%Y-%m-%d" }}</span></a></li>
{% endfor %}
</ul>

{% endfor %}
