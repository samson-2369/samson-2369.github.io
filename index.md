---
title: Home
description: Cornell Security is the portfolio and research site of Norris Cornell, focused on cybersecurity, critical infrastructure, ICS/SCADA, IAM, and satellite cybersecurity.
---

<section class="hero">
  <p class="eyebrow">Cornell Security</p>
  <h1>Cybersecurity research for the systems society depends on.</h1>
  <p>
    Cornell Security is the professional portfolio and research platform of Norris Cornell.
    It brings together work in critical infrastructure defense, ICS / SCADA security,
    satellite cybersecurity, signal trust, identity and access management, and practical cyber defense.
  </p>

  <div class="button-row">
    <a class="button" href="/research/">View Research</a>
    <a class="button secondary" href="/blog/">Read the Blog</a>
    <a class="button secondary" href="/projects/">View Projects</a>
  </div>
</section>

<div class="stat-strip">
  <div class="stat">
    <strong>Research Areas</strong>
    <span>ICS / SCADA, signal trust, RF / satellite, cyber defense</span>
  </div>
  <div class="stat">
    <strong>Professional Focus</strong>
    <span>Critical infrastructure, IAM, blue-team thinking, defensive systems analysis</span>
  </div>
  <div class="stat">
    <strong>Site Purpose</strong>
    <span>Research, portfolio work, technical writing, and professional visibility</span>
  </div>
</div>

## Research highlights

<div class="grid grid-2">
  <div class="card">
    <h3><a href="/research/satellite-cybersecurity-when-cyber-meets-the-spectrum/">Satellite Cybersecurity: When Cyber Meets the Spectrum</a></h3>
    <p>A research-driven look at how SIGINT, ICS, and application security converge around the invisible timing and RF dependencies critical systems already trust.</p>
  </div>

  <div class="card">
    <h3><a href="/research/inputs-lie-your-system-trusts-signals-it-shouldnt/">Inputs Lie: Your System Trusts Signals It Shouldn't</a></h3>
    <p>An analysis of why control systems accept manipulated upstream inputs and how that trust becomes an operational attack surface.</p>
  </div>
</div>

## What you'll find here

<div class="grid grid-3">
  <div class="card">
    <h3>Research & Whitepapers</h3>
    <p>Long-form technical analysis focused on critical infrastructure, RF trust, industrial control systems, and defensive systems thinking.</p>
  </div>

  <div class="card">
    <h3>Blog & Education</h3>
    <p>Readable technical articles that help practitioners, students, and hiring managers understand the why behind the work.</p>
  </div>

  <div class="card">
    <h3>Projects & Portfolio Work</h3>
    <p>Hands-on security projects, Python-based tooling, and practical demonstrations that show applied capability.</p>
  </div>
</div>

## Speaking & professional direction

<div class="panel">
  <p class="page-intro">
    This site also supports public speaking, conference submissions, and professional networking by presenting Norris Cornell's work in a clean, research-forward format.
    It is designed to showcase both depth of thought and practical security understanding.
  </p>
</div>

## Recent writing

<div class="article-list">
{% assign recent_items = site.posts | sort: "date" | reverse %}
{% for post in recent_items limit:3 %}
  <article>
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </article>
{% endfor %}
</div>
