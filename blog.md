---
layout: content_list
title: Blog
permalink: /blog
published: True
---

{% for c in site.content reversed %}

{% if c.layout == "youtube_video" %}
{% include youtube_preview.html title=c.name link=c.link time=c.date url=c.url %}
{% endif %}

{% if c.layout == "blog" %}
{% include post_preview.html url=c.url title=c.name preview=c.excerpt time=c.date author=c.author %}
{% endif %}

{% endfor %}
