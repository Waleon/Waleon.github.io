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

{% for category in site.categories %}<a class="button" href="#{{ category | first }}">{{ category | first }}</a>{% endfor %}

{% for category in site.categories %}

<h2><a id="{{ category | first }}">{{ category | first }}</a></h2>

<h2 class="hr">{{ category | first }}</h2>

<ul class="title-list">
{% for post in category.last %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% include _includes/components/post-list-item.html post=post %}
{% endfor %}
</ul>

{% endfor %}



{% assign post = include.post %}

{% if site.hydejack.use_lsi or site.use_lsi %}
  {% assign related_posts = site.related_posts %}
{% elsif post.categories.first %}
  {% assign related_posts = site.categories[post.categories.first] | where_exp:"post", "post.url != page.url" %}
{% elsif post.tags.first %}
  {% assign related_posts = site.tags[post.tags.first] | where_exp:"post", "post.url != page.url" %}
{% else %}
  {% assign related_posts = site.related_posts %}
{% endif %}

{% if related_posts.size > 0 %}
<aside class="related mb4" role="complementary">
  <h2 class="hr">{{ site.data.strings.related_posts | default:"Related Posts" }}</h2>

  <ul class="related-posts">
    {% for post in related_posts limit:3 %}
      {% include components/post-list-item.html post=post %}
    {% endfor %}
  </ul>
</aside>
{% endif %}