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

{% assign date_formats  = site.data.strings.date_formats                  %}
{% assign list_group_by = date_formats.list_group_by | default:"%Y"       %}
{% assign list_entry    = date_formats.list_entry    | default:"%d %b"    %}
{% assign format        = date_formats.related_post  | default:"%d %b %Y" %}

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

{% for titlea in site.categories[page.title] %}
<h2 class="hr">{{ titlea }}</h2>


{% assign posts = site.categories[page.slug] %}

{% if page.title.size > 0 %}
  <header>
    <h1 class="page-title">{{ page.title }}</h1>
  </header>
  <hr class="sr-only"/>
{% endif %}

{% for post in posts %}
  {% assign currentdate = post.date | date:list_group_by %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h2 id="{{ list_group_by | slugify }}-{{ currentdate | slugify }}" class="hr">{{ currentdate }}</h2>
    <ul class="related-posts">
    {% assign date = currentdate %}
  {% endif %}
  123456
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}
