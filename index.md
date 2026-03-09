---
title: Home
description: Cornell Security is the portfolio and research site of Norris Cornell, focused on cybersecurity, critical infrastructure, and signal‑layer dependencies.
---

<section class="hero">
  <h1>Security research focused on the systems society depends on.</h1>
  <p>
    Cornell Security is the professional portfolio and research platform of Norris Cornell.
    The site brings together work in cyber defense, identity and access management,
    industrial control systems (ICS/SCADA), satellite cybersecurity, and technical writing focused on
    protecting critical infrastructure.
  </p>
  <div class="button-row">
    <a class="button" href="/research/">View Research</a>
    <a class="button secondary" href="/blog/">Latest Articles</a>
  </div>
</section>

## Featured research

<div class="panel">
  <p class="eyebrow">Featured Paper</p>
  <h2><a href="/research/satellite-cybersecurity-when-cyber-meets-the-spectrum/">Satellite Cybersecurity: When Cyber Meets the Spectrum</a></h2>
  <p class="meta">
    <strong>Author:</strong> Norris Cornell · <strong>Category:</strong> Research Paper
  </p>
  <p>
    Critical infrastructure increasingly depends on timing and RF signals that many cybersecurity
    programs do not directly model, validate, or monitor. This paper examines how satellite,
    signal‑layer, and application‑trust assumptions intersect across cyber‑physical systems.
  </p>
  <div class="button-row">
    <a class="button" href="/research/satellite-cybersecurity-when-cyber-meets-the-spectrum/">Read Abstract &amp; Paper</a>
    <a class="button secondary" href="/research/">View Research Archive</a>
  </div>
</div>

## Latest writing

{% assign recent_posts = site.posts | sort: "date" | reverse | slice: 0,3 %}
<div class="grid">
{% for post in recent_posts %}
  <div class="card">
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </div>
{% endfor %}
</div>

## Projects

<p>
  Practical cybersecurity projects and defensive lab environments.
</p>
<div class="button-row">
  <a class="button secondary" href="/projects/">View Projects</a>
</div>