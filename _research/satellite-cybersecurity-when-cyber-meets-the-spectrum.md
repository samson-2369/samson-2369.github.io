---
layout: paper
title: "Satellite Cybersecurity: When Cyber Meets the Spectrum"
date: 2025-07-01
version: "Whitepaper"
description: "How SIGINT, industrial control systems and application security converge around satellite timing and RF dependencies in critical infrastructure."
pdf: /assets/papers/satellite-cybersecurity.pdf
---

## Abstract

Modern society relies on **satellite signals** for everything from cellular timing to financial transactions and power grid synchronisation. These signals are not inherently authenticated or encrypted; they were designed for reliability and availability, not security. As critical infrastructure adopts connected sensors and automation, adversaries can exploit RF‑layer weaknesses to disrupt operations or extract sensitive data. This paper explores the intersection of satellite communications, industrial control systems (ICS) and traditional application security to illuminate new attack surfaces and propose mitigation strategies.

## Introduction

Every smartphone and industrial controller uses timing derived from the Global Positioning System (GPS) or other global navigation satellite systems (GNSS). Many supervisory control and data acquisition (SCADA) systems rely on satellite links for remote telemetry. Yet most cyber hygiene programmes focus on software vulnerabilities and network segmentation, ignoring the trust assumptions baked into **signal‑level infrastructure**. Attackers can jam or spoof GNSS signals, manipulate satellite uplinks and downlinks, and compromise ground stations. In doing so they can cause downstream applications to malfunction or fail silently.

## Attack surface

1. **Signal‑layer manipulation.** GNSS spoofing devices can broadcast false timing or location information that receivers accept as valid. Attacks on power grids have shown that shifting time stamps by a few milliseconds can destabilise control loops.
2. **Uplink/downlink compromise.** Satellite ground stations and transponders often run outdated firmware and rely on weak authentication. Compromising these systems can allow intercepting or injecting traffic into commercial or military communications.
3. **Supply chain vulnerabilities.** Many satellite modems and receivers ship with default credentials or unpatched web interfaces. These devices are installed in field sites with little monitoring.
4. **Application dependency.** Applications that consume satellite‑derived data rarely validate it. GPS time might be assumed trustworthy by a certificate authority, or SCADA software might use position data for asset location without cross‑checking.

## Defensive strategies

* **Signal validation.** Cross‑correlate timing signals from multiple GNSS constellations and terrestrial sources. Use cryptographically authenticated sources where available (e.g., upcoming GPS III M‑code for military use).
* **Hardware trust anchors.** Harden receivers with secure boot, signed firmware and tamper‑resistant modules. Replace default credentials and disable web management interfaces when not needed.
* **Network segmentation.** Treat satellite links as untrusted networks. Place demodulators in a DMZ and inspect traffic before forwarding to internal systems.
* **Anomaly detection.** Monitor signal strength, direction and time‑of‑arrival metrics for anomalies. Deploy spectrum analysis tools to detect jamming or spoofing.
* **Application hardening.** Validate time and location data against independent sources. Implement fail‑safe modes for control systems when signal quality is degraded.

## Conclusion

Satellite dependencies permeate critical infrastructure. Defenders must recognise that **cybersecurity isn’t just about IP packets and software** – it extends to electromagnetic signals and hardware. By understanding the attack surface and adopting a defence‑in‑depth approach that includes signal validation, secure hardware, segmentation and monitoring, we can reduce the risk posed by threats at the intersection of cyber and the spectrum.

## Citation

Cornell, N. (2025). _Satellite Cybersecurity: When Cyber Meets the Spectrum_. Cornell Security Research Archive. https://www.cornellsecurity.com/research/satellite-cybersecurity-when-cyber-meets-the-spectrum

© 2025 Norris Cornell. This research may be cited with attribution. Redistribution or reproduction without permission is prohibited.