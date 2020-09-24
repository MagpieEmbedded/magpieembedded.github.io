---
layout: content_list
title: Content
permalink: /content
published: True
---

{% for c in site.content %}

  {% include youtube_video.html title=c.name link=c.link time=c.date %}

{% endfor %}  

