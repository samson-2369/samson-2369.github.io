---
title: Blog
permalink: /blog/
layout: default
description: Latest articles on cybersecurity, critical infrastructure, and cyber defense.
---

# Blog

<p class="page-intro">
  Articles focused on cybersecurity fundamentals, infrastructure resilience,
  and defensive practice.
</p>

{% for post in site.posts %}
  <article class="post-entry">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p class="meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </article>
{% endfor %}