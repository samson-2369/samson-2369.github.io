---
layout: post
title: "ICS Taught Me More About Input Validation Than OWASP Ever Did"
date: 2026-02-28
categories: [research, appsec]
tags: [ICS, OT, OWASP, input-validation, AppSec, MOVEit, SCADA]
author: Norris Cornell
excerpt: "Before I learned about OWASP or STRIDE, electronics taught me a harsh truth: if a system trusts bad input, it will fail — sometimes violently. ICS and AppSec live in separate worlds, but the problems they face are deeply connected."
series: "When Software Meets the Physical World: AppSec Lessons From ICS"
---

*Part 1 of the "When Software Meets the Physical World: AppSec Lessons From ICS" series*

## Introduction: The Lesson ICS Taught Me Early

Before I entered cybersecurity, I spent nearly 20 years as an electronics technician working with sensors, control circuits, and embedded systems. When I started researching SCADA and ICS security for my graduate work, I recognized something familiar: the same trust failures I'd seen at the hardware level — sensors lying, signals drifting, inputs causing unexpected system behavior.

Long before I learned about OWASP, STRIDE, or secure design patterns, electronics taught me a harsh truth:

**"If a system trusts bad input, it will fail — sometimes violently."**

As I transitioned deeper into cybersecurity, I realized that the same input validation failures that break modern web applications have been plaguing ICS environments for decades — they just look different. ICS and AppSec often live in separate worlds, but the problems they face are deeply connected. This series explores how lessons from one domain can strengthen the other.

## The 2023 MOVEit Wake-Up Call

One of the largest AppSec failures in recent memory didn't require sophisticated malware or zero-days. It began with something simpler — a trust failure.

When attackers breached MOVEit Transfer in 2023, they exploited a straightforward SQL injection vulnerability. The flaw allowed malicious users to bypass authentication, execute arbitrary SQL queries, and exfiltrate data — all because the application trusted a user-controlled parameter.

The result:
- Over 2,000 organizations compromised
- 77 million individuals affected
- Financial, healthcare, and government entities impacted

A single unsanitized parameter triggered one of the most widespread breaches in a decade.

**The MOVEit breach is textbook AppSec. But the underlying failure isn't unique to software.**

## The ICS Version of the Same Problem

In ICS, input validation failures don't look like SQL injection — they look like unsafe setpoints.

An operator enters: "Set temperature to 150°C."

If the controller doesn't validate that 150°C exceeds the safe operating limit for that vessel's pressure rating, it executes the command anyway. No physics checks. No boundary verification. Just blind trust.

This pattern repeats across control networks:
- Unsafe setpoints accepted without validation
- Timing values that violate process constraints (e.g., opening a valve before equalizing pressure)
- State transitions that bypass interlocks

The consequences in ICS are immediate and physical: equipment damage, safety incidents, environmental impact.

Different domain. Same failure mode.

## OWASP vs. ICS: Two Domains, One Lesson

When OWASP publishes its Top 10, developers see categories like:

- **A03:2021 — Injection:** SQL, command, or XSS injection
- **A04:2021 — Insecure Design:** Missing input boundary checks, unsafe parameter handling

ICS engineers see the same thing through a different lens:

| OWASP Failure | ICS Equivalent |
|--------------|----------------|
| SQLi, XSS, command injection | Dangerous setpoints accepted without validation |
| Insecure design | Unsafe state transitions or timing errors |
| Trusting input | Trusting sensors, operators, or unverified data |

In both cases, systems trust data that can lie — and attackers exploit that trust.

## What ICS Taught Me About AppSec

ICS environments forced me to see input validation differently. It's not just about sanitizing fields — it's about understanding that external data is adversarial by default.

**1. External data is hostile until proven otherwise.**
Whether it's a user form field or a sensor reading, treat all inputs as potentially malicious.

**2. Validation is about context, not format.**
"150°C" passes every syntax check — but it's unsafe if the vessel's pressure rating maxes out at 120°C. The input is valid; the operation isn't.

**3. Unsafe transitions are more dangerous than unsafe values.**
A state change at the wrong time can cause more damage than a bad value.

**4. The blast radius changes — physical in ICS, digital in software.**
But the fundamental security principle remains the same.

## The Universal Takeaway

Whether you're building APIs, mobile apps, or industrial systems — the lesson holds:

**Validate everything. Trust nothing. Design for hostility.**

ICS environments experience the consequences of trust failures in real time — AppSec just has the luxury of logs instead of smoke.

---

*Coming Next: Part 2 — Broken Access Control. In both ICS and AppSec, attackers don't always break in; sometimes, they just ask politely and systems let them.*

---

*Norris Cornell works in Identity and Access Management as a Technical Lead, with nearly 20 years of electronics technician experience. He specializes in the convergence of RF/SIGINT, ICS/OT security, and cyber-physical systems. He presented "When Cyber Meets the Spectrum" at BSides Delaware 2025.*
