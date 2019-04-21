---
layout: default
title: Atur Garg's blog
---

{{ page.title }}
================

{% for post in site.posts %}*   {{ post.date | date\_to\_string }} [{{ post.title }}]({{ post.url }} "{{ post.title }}")
{% endfor %}