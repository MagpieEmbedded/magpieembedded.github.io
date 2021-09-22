---
layout: content_list
title: Content
permalink: /content
published: True
---

{% for c in site.content reversed %}

{% if c.type == "youtube_video" %}
{% include youtube_preview.html title=c.name link=c.link time=c.date %}
{% endif %}

{% if c.type == "blog" %}
{% include post_preview.html url=c.url title=c.name preview=c.excerpt time=c.date author=c.author %}
{% endif %}

{% endfor %}
