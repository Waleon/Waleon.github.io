---
layout: page
title: 关于
description: 谈天、说地、侃代码、开车
keywords: Liang Wang, 王亮
comments: true
menu: 关于
permalink: /about/
---

进步始于交流， 收获源于分享。

纯正开源之美，有趣、好玩、靠谱。。。~O(∩_∩)O~

## 联系方式

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## 擅长领域

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
