---
layout: paper
title: "Inputs Lie: Your System Trusts Signals It Shouldn't"
date: 2025-12-02
version: "Article"
description: "How industrial control systems faithfully execute on manipulated inputs — and why the signals layer is the gap nation-state actors mapped before most defenders knew to look."
pdf: /assets/papers/inputs-lie.pdf
---

In December 2015, KAMACITE — the Russian threat actor Dragos tracks as a Stage 2 ICS adversary — coordinated one of the most consequential cyberattacks on critical infrastructure ever recorded. Three Ukrainian power distribution companies lost power simultaneously. 230,000 customers went dark.

The malware that did it wasn't sophisticated at the network layer. It didn't need to be.

It manipulated the inputs.

SCADA operators watched their HMIs show normal system states while breakers were being tripped remotely. The control systems executed faithfully — because the signals they received said to. By the time human operators understood what was happening, the damage was done.

> *The ICS didn't fail because the network was breached. It failed because it trusted inputs it had no way to verify.*

A few months ago I wrote about how satellite signals — GPS, GNSS, RF — are largely undefended against spoofing and manipulation. The gap isn't just theoretical. It lives inside your industrial control systems, and KAMACITE proved it almost a decade ago.

This is where that series continues.

## The Real Starting Point of Every Control Loop

Most ICS/OT security conversations happen inside the perimeter: PLC hardening, segmentation, protocol validation. All important — and they're where the industry has focused because that's where defenders have tools, visibility, and leverage.

But every one of those controls starts after the actual beginning of every control decision.

Before a single rung of logic executes, your system is already trusting inputs it never validated:

- GPS timing signals coordinating protective relays and substation synchronization
- GNSS for precise clock cycles in time-sensitive automation sequences
- External NTP servers — usually without authentication — keeping PLCs in sync
- Satellite or RF channels used as "trusted transport" for remote commands
- Raw sensor telemetry from field devices that cannot self-verify their own integrity

These signals enter the system upstream of every security control you've built. They're the foundation every decision rests on — and they were designed for reliability in a different era, against different threats.

The systems are still running on those inherited assumptions. The threat actors adapted faster.

## The Digital Logic Truth

Here's what connects traditional cybersecurity to OT at a fundamental level: PLCs and RTUs are deterministic digital logic. They don't think. They evaluate.

If inputs are wrong, outputs are wrong. That's not a bug — it's how deterministic systems are designed to work.

> *A corrupted GPS timing signal doesn't "confuse" a protective relay. It forces a specific state. A spoofed sensor value doesn't make an RTU hesitate — it flips a bit in a digital register, and logic executes accordingly.*

The PLC has no mechanism for distinguishing truth from a well-crafted lie. If you can control what the system believes about its inputs, you control what the system does — without ever touching the logic itself.

This is what VOLTZITE is doing right now. Dragos's 2025 Year in Review documents VOLTZITE at Stage 2 — actively investigating what inputs cause industrial processes to stop. They're not trying to write malware. They're mapping the input layer.

The operator staring at the HMI sees what the compromised signals tell them. They make decisions based on a fictional reality. From there, consequences cascade into the physical world.

## Why This Gap Is Structural

You can't retrofit authentication into 20-year-old GPS receivers without breaking the timing precision the entire grid synchronization depends on. You can't patch GNSS clock synchronization without risking the availability your operation requires to stay online.

This isn't a failure of security programs. It's how the discipline developed.

Traditional ICS/OT security focuses where defenders have leverage: inside the perimeter, where you control the logic and the communications. The signals layer sits upstream — in infrastructure that evolved for different purposes, operated by different teams, under different assumptions about who the adversary was.

KAMACITE, ELECTRUM, and VOLTZITE understand this asymmetry. They operate below the detection floor of every framework currently deployed in critical infrastructure. MITRE ATT&CK for ICS documents what they do at the network and logic layers — but has no techniques for physical-layer signal manipulation. NERC CIP has no requirements for GNSS timing integrity monitoring. CISA's Known Exploited Vulnerabilities catalog has no entries for GPS spoofing.

> *The gap isn't in your tools. The gap is in the threat model — and nation-state actors mapped it years before most defenders knew to look.*

## Detection Without Replacement

Here's what matters for defenders: you don't need to tear out your legacy infrastructure to start closing this gap.

Signal-layer threats leave traces — if you're looking for them:

- **Timing anomalies** — Discrepancies between redundant clocks or GPS receivers that don't reconcile with each other or with physical reality
- **Sensor consistency failures** — Redundant field sensors reporting divergent values with no physical explanation
- **GNSS/NTP drift** — Sudden unexplained shifts in timing that don't correlate with known infrastructure changes
- **RF environment changes** — Patterns that don't align with expected site conditions
- **Operator intuition** — Someone noticing something "feels wrong" with sensor readings even though no alarm fired. This is a signal, not noise.

The common thread is better observability at the signals layer, not new hardware. Most organizations already collect this data in some form. The question is whether anyone is looking at it through an adversarial lens.

## What This Means for Your Infrastructure

If your critical operations depend on any external signal — timing, positioning, navigation, or remote commands — you are running on inputs you have probably never threat-modeled for spoofing, replay, or manipulation.

Dragos's 2025 report found that 82% of OT organizations have no clear criteria for when an operational anomaly should trigger a cyber investigation. That means most environments cannot distinguish between a system behaving strangely and a system being attacked at the inputs layer. By the time they figure it out, the forensic data that would explain what happened is already gone.

That's the structural problem the Inputs Lie framework is designed to address.

> *The question isn't whether your perimeter is hardened. It's whether you've ever threat-modeled the signals your system trusts before it reaches the perimeter.*

## Next in This Series

Next: how PLCs and RTUs actually fail under adversarial conditions — and what deterministic logic executing on manipulated inputs means for your detection strategy.

For now, start here:

- Map where your operations touch external signals — GPS, NTP, GNSS, RF, satellite links, field sensor telemetry
- Ask which of those signals your security program has threat-modeled for spoofing, replay, or manipulation
- For any you haven't: that's your gap. That's where VOLTZITE is looking

The invisible layer defenders overlook is becoming the layer attackers exploit. Let's make it visible.

---

*Norris Cornell is a cybersecurity professional specializing in IAM, ICS/OT, and satellite cybersecurity. Speaker at BSides Delaware 2025. Research and full framework at CornellSecurity.com.*
