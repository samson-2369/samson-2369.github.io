
---
title: Home
---

# Cornell Security

Cybersecurity research and portfolio of **Norris Cornell**.

Focus areas include:

- Critical Infrastructure Security
- ICS / SCADA Security
- Satellite Cybersecurity
- Identity and Access Management
- Cyber Defense

## Featured Research

### [Satellite Cybersecurity: When Cyber Meets the Spectrum](/research/satellite-cybersecurity/)

Research exploring how satellite timing and RF signal trust intersect with critical infrastructure cybersecurity.

[View Research Archive](/research/)

## Latest Writing

{% for post in site.posts limit:3 %}

### [{{ post.title }}]({{ post.url }})

{{ post.excerpt }}

{% endfor %}

## Projects

Practical cybersecurity projects and defensive lab environments.

[View Projects](/projects/)
