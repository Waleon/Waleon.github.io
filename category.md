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
{% assign format        = date_formats.related_post  | default:"%d %b %Y" %}

{% for category in site.categories %}
<h2 class="hr">{{ category | first }}</h2>
{% assign category_start     = site.data.strings.category_start     | default:"in " %}
{% assign tag_start          = site.data.strings.tag_start          | default:"on " %}
{% assign category_separator = site.data.strings.category_separator | default:" / " %}
{% assign tag_separator      = site.data.strings.tag_separator      | default:", "  %}
{% include components/tag-list.html tags=post.categories meta=site.featured_categories start_with=category_start separator=category_separator %}
{% include components/tag-list.html tags=post.tags meta=site.featured_tags start_with=tag_start separator=tag_separator %}

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
