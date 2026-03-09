---
title: Research
permalink: /research/
description: Research archive and whitepapers by Norris Cornell on satellite cybersecurity, ICS/OT, signal trust, and critical infrastructure defense.
---

# Research Archive

<p class="page-intro">
  This section contains technical research and whitepaper-style analysis focused on critical infrastructure,
  signal-layer dependencies, industrial trust assumptions, and defensive systems thinking.
</p>

<div class="article-list">
{% assign sorted_research = site.research | sort: "date" | reverse %}
{% for paper in sorted_research %}
  <article>
    <h3><a href="{{ paper.url }}">{{ paper.title }}</a></h3>
    <p class="meta">
      {{ paper.date | date: "%B %-d, %Y" }}{% if paper.version %} · {{ paper.version }}{% endif %}{% if paper.category %} · {{ paper.category }}{% endif %}
    </p>
    <p>{{ paper.description }}</p>
  </article>
{% endfor %}
</div>
