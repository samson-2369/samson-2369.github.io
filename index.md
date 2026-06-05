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

<div class="panel">
  <p class="eyebrow">Four-Part Series</p>
  <h2>Inputs Lie</h2>
  <p>
    A research series examining how critical infrastructure fails when systems implicitly trust
    unverifiable inputs — from physical sensors and RF signals through PLC control logic to
    API endpoints. Each part builds on the last, culminating in a live detection lab.
  </p>
  <ol>
    <li><a href="/research/inputs-lie-your-system-trusts-signals-it-shouldnt/">Part 1 — Your System Trusts Signals It Shouldn’t</a></li>
    <li><a href="/research/inputs-lie-part-2-kamacite-voltzite-and-the-signals-gap/">Part 2 — KAMACITE, VOLTZITE, and the Signals Gap</a></li>
    <li><a href="/research/inputs-lie-part-3-logic-follows-lies/">Part 3 — Logic Follows Lies: How PLCs and RTUs Execute Adversarial Intent</a></li>
    <li><a href="/research/inputs-lie-part-4-detecting-lies-at-the-signal-layer/">Part 4 — Detecting Lies at the Signal Layer</a></li>
  </ol>
  <div class="button-row">
    <a class="button" href="/research/inputs-lie-your-system-trusts-signals-it-shouldnt/">Start Reading</a>
    <a class="button secondary" href="/research/">View All Research</a>
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
