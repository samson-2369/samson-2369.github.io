---
title: Research
permalink: /research/
layout: default
description: Research archive and whitepapers by Norris Cornell on satellite cybersecurity, signal trust, and critical infrastructure defense.
---

# Research Archive

<p class="page-intro">
  This archive contains long‑form research, whitepapers, and technical analysis focused on
  critical infrastructure, signal trust, RF‑layer dependencies, and defensive systems thinking.
</p>

<div class="article-list">
{% assign papers = site.research | sort: "date" | reverse %}
{% for paper in papers %}
  <article class="research-entry">
    <p class="paper-type">Research Paper</p>
    <h2><a href="{{ paper.url }}">{{ paper.title }}</a></h2>
    <p class="meta">
      <strong>Author:</strong> Norris Cornell · <strong>Published:</strong> {{ paper.date | date: "%B %-d, %Y" }}
      {% if paper.version %} · <strong>Version:</strong> {{ paper.version }}{% endif %}
    </p>
    {% if paper.description %}
    <p>{{ paper.description }}</p>
    {% endif %}
    <div class="button-row">
      <a class="button secondary" href="{{ paper.url }}">Read Paper</a>
      {% if paper.pdf %}
      <a class="button" href="{{ paper.pdf }}">Download PDF</a>
      {% endif %}
    </div>
  </article>
{% endfor %}
</div>