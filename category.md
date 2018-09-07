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

{% assign date_formats  = site.data.strings.date_formats               %}
{% assign format = date_formats.related_post | default:"%d %b %Y" %}

{% for category in site.categories %}<a class="button" href="#{{ category | first }}">{{ category | first }}</a>{% endfor %}

{% for category in site.categories %}
<h2 class="hr">{{ category | first }}</h2>

<ul class="title-list">
{% for post in category.last %}
<li>
  <a href="{{ post.url | relative_url }}" class="h4 flip-title">
    <span>{{ post.title }}</span>
  </a>
  <time class="heading faded fine" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date:format }}</time>
</li>
{% endfor %}
</ul>

{% endfor %}
