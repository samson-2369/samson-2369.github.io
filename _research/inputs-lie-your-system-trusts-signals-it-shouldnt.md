---
layout: paper
title: "Inputs Lie: Your System Trusts Signals It Shouldn't"
date: 2025-07-12
version: "Research Paper"
description: "Examining how industrial systems faithfully execute malicious or erroneous inputs and why defenders must gain visibility into signal‑layer truth."
pdf: /assets/papers/inputs-lie.pdf
---

## Abstract

Industrial control systems (ICS), building automation and even modern cloud platforms rely on data inputs from sensors and upstream systems. These signals – temperature readings, pressure values, GPS timestamps, heartbeats – are often **treated as gospel**. Yet attackers can manipulate or forge these inputs to cause systems to behave unpredictably. This paper explores the philosophy that _inputs lie_, surveys examples of manipulated signals leading to incidents, and presents strategies to make systems more resilient to false data injection.

## Introduction

Traditional cybersecurity focuses on protecting the boundaries of a system: authenticating users, patching software vulnerabilities, and encrypting data. But inside that protected boundary, the code and logic often assume that **incoming data reflects reality**. Programmable logic controllers (PLCs) accept sensor values without validation. Cloud services integrate third‑party APIs without verifying data integrity. This blind trust allows adversaries to trigger destructive or subtle behaviours simply by **lying** through sensors or messages.

## Case studies

1. **Stuxnet's speed sensors.** The infamous malware manipulated centrifuge rotational speed readings so that the supervisory system saw normal values while the hardware spun too fast or too slow. Engineers were blind to the sabotage because the inputs lied.
2. **SCADA pressure spoofing.** In a simulated water system, researchers injected false pressure readings into a PLC. The logic believed pressure was dropping and opened valves further, causing actual pressure to spike and damage equipment.
3. **API data poisoning.** Attackers have manipulated stock prices in algorithmic trading systems by feeding false quotes into APIs. Trading bots reacted to bogus market data, causing real financial loss.

## Why inputs lie

- **Lack of authentication.** Sensors and remote terminals often broadcast values in cleartext over serial or radio protocols. Anyone with RF equipment can inject their own packets.
- **Poor sanity checking.** Logic often fails to validate ranges, rates of change or cross‑correlations between related measurements.
- **Complex dependencies.** Systems pull data from nested services (e.g., a map API relying on GPS) that can each be compromised.

## Making systems less gullible

* **Redundant sensing.** Use multiple sensors with diverse modalities (e.g., pressure and flow rate) to cross‑validate readings.
* **Check plausibility.** Implement rate‑of‑change limits and sanity checks. If a temperature reading jumps 50 °C in a second, disregard it until further corroboration.
* **Cryptographically authenticate signals.** Where possible, use signed messages or challenge‑response protocols for remote sensors.
* **Monitor for anomalies.** Behavioural analytics can detect when control loops are responding in ways inconsistent with physical laws.
* **Fail safe.** Default to safe states (shutdown, manual override) when sensor data becomes suspect rather than optimistically continuing.

## Conclusion

Software will always behave in accordance with its inputs. Attackers exploit this by lying through sensors, APIs and upstream systems. Defenders must broaden the definition of cybersecurity to include **assuring the truth of the data that drives our logic**. Only by recognising that inputs can and will lie can we build systems resilient to deception.

## Citation

Cornell, N. (2025). _Inputs Lie: Your System Trusts Signals It Shouldn't_. Cornell Security Research Archive. https://www.cornellsecurity.com/research/inputs-lie-your-system-trusts-signals-it-shouldnt

© 2025 Norris Cornell. This research may be cited with attribution. Redistribution or reproduction without permission is prohibited.