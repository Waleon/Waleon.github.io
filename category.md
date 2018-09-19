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

{% assign tags = post.tags %}
{% assign meta = site.featured_tags %}
{% assign start_with = tag_start %}
{% assign separator = tag_separator %}
{% assign end_with = include.end_with %}

{% assign content = '' %}

{% if tags.size > 0 %}
  {% assign content = start_with %}
  {% for tag_slug in tags %}
	<h2 class="hr">{{ tag_slug}}</h2>
	<h2 class="hr">{{ tag_slug | first }}</h2>
    {% capture iter_separator %}{% if forloop.last %}{{ end_with }}{% else %}{{ separator }}{% endif %}{% endcapture %}

    {% assign tag = meta | where: "slug", tag_slug | first %}

    {% if tag %}
      {% capture content_temp %}{{ content }}<a href="{{ tag.url | relative_url }}" class="flip-title">{{ tag.title }}</a>{{ iter_separator }}{% endcapture %}
    {% else %}
      {% capture content_temp %}{{ content }}<span>{{ tag_slug | capitalize }}</span>{{ iter_separator }}{% endcapture %}
    {% endif %}

    {% assign content = content_temp %}
  {% endfor %}
{% endif %}

{{ content }}




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
