---
title: Research
permalink: /research/
description: Research archive and whitepapers by Norris Cornell on cybersecurity, critical infrastructure, RF/satellite security, and ICS/SCADA defense.
---

## Research Archive

This section contains technical research and whitepapers focused on cybersecurity, critical infrastructure protection, signal-layer dependencies, and defensive systems thinking.

<div class="article-list">
  {% assign sorted_research = site.research | sort: "date" | reverse %}
  {% for paper in sorted_research %}
    <article>
      <h3><a href="{{ paper.url | relative_url }}">{{ paper.title }}</a></h3>
      <div class="meta">{{ paper.date | date: "%B %-d, %Y" }}{% if paper.version %} · {{ paper.version }}{% endif %}{% if paper.category %} · {{ paper.category }}{% endif %}</div>
      <p>{{ paper.abstract | default: paper.description }}</p>
    </article>
  {% endfor %}
</div>
