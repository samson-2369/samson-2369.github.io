---
title: Blog
permalink: /blog/
description: Blog articles by Norris Cornell on cyber hygiene, critical infrastructure, OT visibility, and cyber defense practice.
---

# Blog

<p class="page-intro">
  Articles focused on cybersecurity fundamentals, cyber defense practice, infrastructure resilience,
  and the practical realities behind defensive work.
</p>

<div class="article-list">
{% assign sorted_posts = site.posts | sort: "date" | reverse %}
{% for post in sorted_posts %}
  <article>
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </article>
{% endfor %}
</div>
