---
layout: paper
title: "Inputs Lie: Your System Trusts Signals It Shouldn't"
date: 2025-12-02
version: "Article · Part 1 of 3"
description: "If you lie to an industrial system about its inputs, it will execute that lie faithfully into the physical world. The first article in the Inputs Lie series."
pdf: /assets/papers/inputs-lie.pdf
---

*Inputs Lie Series · Part 1 of 3*

If you lie to an industrial system about its inputs, it will execute that lie faithfully into the physical world. No hesitation. No intuition. Just deterministic logic doing exactly what it was designed to do.

In my last post, I talked about how satellite signals — GPS, GNSS, RF — are largely undefended against spoofing and manipulation. The gap isn't just theoretical. It lives inside your industrial control systems.

## The Perimeter Is Not the Starting Point

Most ICS/OT security conversations happen inside the perimeter: PLC hardening, segmentation, protocol validation. All important — and they're where the industry has focused because that's where defenders have tools, visibility, and leverage.

But every one of those controls starts after the actual beginning of every control decision.

Before a single rung of logic executes, your system is already trusting inputs it never validated:

- GPS timing signals coordinating protective relays and substation synchronization
- GNSS for precise clock cycles in time-sensitive automation sequences
- External NTP servers — usually without authentication — keeping PLCs in sync
- Satellite or RF channels used as "trusted transport" for remote commands
- Raw sensor telemetry from field devices that cannot self-verify their own integrity

These signals enter the system upstream of every security control you've built.

## Deterministic Logic Has No Skepticism

PLCs and RTUs don't think. They evaluate. Feed them wrong inputs and they produce wrong outputs — not because they failed, but because they worked exactly as designed.

This is the core of the Inputs Lie framework: the gap isn't in the logic, the network controls, or the authentication layer. The gap is upstream of all of it, at the boundary where physical reality becomes digital data.

> *Your system will faithfully execute a lie if the lie arrives in the right format.*

## What This Series Covers

This is Part 1 of a three-part series:

- **Part 1 (this article)** — The foundational concept: why deterministic systems are structurally vulnerable to input manipulation
- **Part 2** — How nation-state actors exploit this gap today, and what defenders can detect without replacing legacy infrastructure
- **Part 3** — How PLCs and RTUs actually fail under adversarial conditions, and what that means for your detection strategy

The invisible layer defenders overlook is becoming the layer attackers exploit. Let's make it visible.

---

*Norris Cornell is a cybersecurity professional specializing in IAM, ICS/OT, and satellite cybersecurity. Speaker at BSides Delaware 2025. Research and full framework at CornellSecurity.com.*
