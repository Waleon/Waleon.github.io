---
layout: page
title: 链接
description: 没有链接的博客是孤独的
keywords: 友情链接
comments: true
menu: 链接
permalink: /links/
---

> 上天决定了谁是你的亲戚，好在我们可以自己选择朋友。

{% for link in site.data.links %}
* [{{ link.name }}]({{ link.url }})
{% endfor %}
