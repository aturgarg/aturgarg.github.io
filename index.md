---
layout: default
title: Atur Garg's blog
---

{{ page.title }}
================

{% for post in site.posts %}*   {{ post.date | date_to_string }} [{{ post.title }}]({{ post.url }})
{% endfor %}


[//]: #  {% for category in site.categories %}
 
[//]: #  ### {{ category[0] }}
 
[//]: #  {% for post in category[1] %}*   [{{ post.title }}]({{ post.url }})
[//]: #  {% endfor %}

[//]: #  {% endfor %}