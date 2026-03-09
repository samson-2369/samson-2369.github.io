---
title: Blog
permalink: /blog/
description: Cybersecurity articles and technical writing by Norris Cornell on cyber defense, ICS/SCADA security, satellite cybersecurity, and critical infrastructure.
---

## Blog

{% for post in site.posts %}
<article>
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  <div class="meta">{{ post.date | date: "%B %d, %Y" }}</div>
  <p>{{ post.excerpt }}</p>
</article>
{% endfor %}
