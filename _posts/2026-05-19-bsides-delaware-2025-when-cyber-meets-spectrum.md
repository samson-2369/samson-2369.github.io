---
layout: post
title: "When Cyber Meets the Spectrum: SIGINT and Security Lessons for ICS Satellite Communications"
subtitle: "BSides Delaware 2025 — Independent Research on AppSec, OT/ICS, and Signals Intelligence Convergence"
date: 2026-05-19
original_presentation_date: 2025-11-01
author: Norris P. Cornell, Jr.
categories: research presentations ics-ot sigint critical-infrastructure
tags: satellite cybersecurity gnss-spoofing ics-security signals-intelligence api-security threat-convergence
featured: true
---

# When Cyber Meets the Spectrum

## Independent Research on the Convergence of AppSec, OT/ICS, and SIGINT

**Originally Presented:** November 2025 at BSides Delaware  
**Research Timeline:** Independent research, conducted and presented prior to formal research collaborations  
**Speaker:** Norris P. Cornell, Jr.  
**Research Focus:** Critical infrastructure security, signals-layer threat analysis, industrial control system vulnerabilities

---

## Executive Summary

This presentation identifies and documents a **critical, previously under-defended attack surface** that emerges at the intersection of three traditionally siloed security domains:

- **Application Security (AppSec)** — Software vulnerabilities, API flaws, input validation failures
- **Operational Technology / Industrial Control Systems (OT/ICS)** — SCADA systems, PLCs, industrial protocols, safety-critical devices
- **Signals Intelligence (SIGINT)** — RF spoofing, jamming, timing attacks, GNSS manipulation, satellite communications

### The Core Finding

**Systems can have strong API security AND solid industrial control system defenses, yet still fail catastrophically if they trust unverified signals at the RF/timing layer.**

When attackers exploit the convergence of these three domains simultaneously, they operate in a blind spot that traditional security frameworks miss — because that blind spot falls between organizational silos and defensive responsibilities.

---

## Why This Research Matters

### The Problem Statement

1. **RF-Layer Blind Spot**
   - Network firewalls cannot detect spectrum-layer manipulation
   - Traditional cybersecurity tools start at the network layer, missing attacks that occur at the RF layer
   - Critical systems implicitly trust signals from satellites, GNSS receivers, and communications systems without verification

2. **ICS Protocol Weaknesses**
   - Many operational technology protocols (Modbus, DNP3, legacy SCADA) transmit data in plaintext
   - No built-in authentication or integrity checking
   - Vulnerable to command injection and data spoofing

3. **Organizational Blind Spot**
   - AppSec teams don't typically defend OT systems
   - OT teams don't typically monitor RF/signal layer threats
   - SIGINT/RF specialists don't typically defend critical infrastructure
   - The convergence zone has **no owner**

### Real-World Evidence

#### Viasat Attack (2022)
- Attackers gained VPN access to satellite ground control network
- Deployed AcidRain wiper malware to thousands of satellite modems
- Cascading outages across European power grids and wind farms
- **Lesson:** Convergence of IT (VPN compromise) + OT (satellite control) + network (widespread deployment) = catastrophic failure

#### Ukraine GPS Warfare (2025 - Active)
- **1,200+ documented GPS disruptions in 2025 alone**
- **300+ "ghost ships" per month** (false AIS data from GPS spoofing)
- **2-3 second timing delays** disrupting power grid automation
- **Proof:** RF-layer attacks are operational, not theoretical
- **Impact:** Directly affecting SCADA timing synchronization, maritime navigation, communications infrastructure

#### UT Austin GPS Spoofing Research
- Demonstrated low-cost GPS spoofing using $3,000 software-defined radio
- Successfully spoofed GPS-guided yacht without triggering any alarms
- Proved that critical infrastructure trusts signals without validation
- **Today:** Similar spoofing kits can be built for under $500

---

## The Hybrid Attack Surface: How the Domains Converge

### Three Domains on a Venn Diagram

When you map AppSec, OT/ICS, and SIGINT threats, the intersection zone represents a critical gap in how we defend critical infrastructure.

### Attack Vectors Across the Convergence

#### AppSec ∩ SIGINT
- API endpoints that process timing or location data become vulnerable to RF spoofing
- False GPS coordinates fed through APIs trigger incorrect automation
- Example: Weather station API spoofed via GNSS → sends false data to control systems → triggers wrong actions

#### ICS/OT ∩ SIGINT
- SCADA systems relying on satellite timing become targets for RF attacks
- Timing synchronization loss cascades across interconnected industrial systems
- Example: Power grid timing synchronization lost due to GPS spoofing → relay timing skew → phase angle errors → grid instability

#### AppSec ∩ ICS/OT
- APIs controlling or monitoring industrial systems inherit both software and industrial vulnerabilities
- Legacy OT protocols exposed through modern API interfaces
- Example: REST API wrapping Modbus commands → API vulnerabilities expose raw industrial control

#### All Three (AppSec ∩ OT/ICS ∩ SIGINT)
- **The Most Dangerous Zone**
- API vulnerability + RF spoofing + weak OT protocol = total system compromise
- Attacker manipulates RF signals → corrupted data enters API → triggers unsafe commands to field devices
- Example: Satellite link spoofed → bad timing data hits weather API → weather API feeds false conditions to substation automation → substation reacts to false readings

---

## Presentation Contents

### Slide Overview

1. **The Invisible Layer** — Introduction to signal-dependent systems
2. **About the Speaker** — Background and credibility context
3. **Talk Scope** — What this is and isn't (awareness, not attack walkthroughs)
4. **Three Domains Collide** — Venn diagram of AppSec, OT/ICS, SIGINT convergence
5. **Cyber-Physical Stack** — SCADA as brain, communications as nervous system, field devices as muscles
6. **IT vs OT Security Priorities** — Why traditional IT security misses OT-specific threats
7. **The Satellite Blind Spot** — Three fundamental gaps in current defenses
8. **Viasat Attack Timeline** — Case study of IT-OT-Network convergence failure
9. **UT Austin GPS Spoofing** — Low-cost RF attack demonstrated on critical systems
10. **Traditional vs Satellite Attacks** — Why network defenses fail at RF layer
11. **GNSS Spoofing 101** — How attackers broadcast false GPS signals
12. **Timing Attacks** — How 2-3 second GPS delays cascade through systems
13. **When the Orchestra Falls Out of Sync** — Metaphor for timing-dependent system failure
14. **When the Dominoes Start to Fall** — Cascade failure in interconnected systems
15. **Ukraine: Live GPS Warfare Testbed** — Active threat evidence (1,200+ disruptions)
16. **Hybrid Attack Surface** — Full convergence framework with RF, network, and application layers
17. **Defense-in-Depth Strategy** — Four-layer defense across RF, network, application, and operational
18. **Monday-Morning Actions** — Immediately actionable steps for defenders
19. **Resources & Acknowledgments** — Standards, communities, and reference materials
20. **Key Takeaways** — Visibility, Validation, Action
21. **Thank You / Contact** — Speaker information

---

## Defense Framework: Four Layers

### Layer 1: RF Layer Defense
- **GNSS hardening** — Authenticate satellite signals
- **Spectrum monitoring** — Detect jamming and spoofing attempts
- **Signal validation** — Verify authenticity before accepting timing data
- **Tools:** SDR monitoring, GNSS receivers with spoofing detection, RF monitoring systems

### Layer 2: Network Layer Defense
- **SATCOM DMZs** — Isolate satellite communications from critical systems
- **Encryption** — Protect data in transit from satellites
- **Segmentation** — Separate timing-critical systems from general network traffic
- **Tools:** Network segmentation, encrypted VPNs for satellite links, edge firewalls

### Layer 3: Application Layer Defense
- **Timestamp validation** — Verify timing data against multiple sources
- **Input sanitization** — Reject obviously false timing or location data
- **Anomaly detection** — Alert when timing deviates from expected patterns
- **Tools:** API input validation, machine learning anomaly detection, timing redundancy checks

### Layer 4: Operational Defense
- **Operator training** — Prepare teams for degraded satellite conditions
- **Tabletop exercises** — Practice responding to RF-layer attacks
- **Degraded operation procedures** — Maintain safety when signals are unavailable
- **Monitoring culture** — Make RF-layer threats visible to operational staff

---

## Immediate Actions for Defenders

### This Week
1. **Add satellites to threat models**
   - Document systems that depend on GPS timing or satellite communications
   - Identify single points of failure related to RF signals

2. **Inventory your dependencies**
   - Which systems rely on GNSS for synchronization?
   - Which systems depend on satellite communications?
   - Where are the gaps in monitoring?

3. **Start with one control**
   - Implement timestamp validation in one critical system
   - Deploy RF monitoring in one satellite ground station
   - Choose one actionable step and deploy this week

### This Month
1. **Expand threat modeling** to include RF-layer attacks
2. **Document signal redundancy** — Can your systems operate without satellites?
3. **Begin operator training** on satellite dependency and failure modes

### This Quarter
1. **Implement network segmentation** for satellite-dependent systems
2. **Deploy spectrum monitoring** for critical infrastructure
3. **Establish operational procedures** for degraded satellite conditions

---

## Connections to Broader Research

This presentation builds directly on the **Inputs Lie** framework — the thesis that critical infrastructure systems fail when they trust unverified inputs across the physics, signals, and application layers.

**The Inputs Lie Series:**
- [Part 1: Your System Trusts Signals It Shouldn't]({{ site.baseurl }}/posts/inputs-lie-part-1)
- [Part 2: KAMACITE, VOLTZITE, and the Signals Gap]({{ site.baseurl }}/posts/inputs-lie-part-2)
- [Part 3: Logic Follows Lies]({{ site.baseurl }}/posts/inputs-lie-part-3)
- [Part 4: Detection at the Signal Layer]({{ site.baseurl }}/posts/inputs-lie-part-4)

**Key Insight:** The convergence of AppSec, OT/ICS, and SIGINT is the practical manifestation of the Inputs Lie framework in action. Every attack vector exploits a system that trusts unverified inputs at one of these three layers.

---

## Download the Complete Presentation

### Full Slide Deck

[**Download: When Cyber Meets the Spectrum (PPTX)**]({{ site.baseurl }}/assets/presentations/bsides-2025/When_Cyber_Meets_the_Spectrum_BSidesDE2025.pptx)

**File Details:**
- Format: Microsoft PowerPoint (.pptx)
- Original Creation: November 2025
- Presentation Date: November 2025 (BSides Delaware)
- Size: ~22 MB (includes high-resolution imagery and technical diagrams)
- Compatibility: PowerPoint, Google Slides, Keynote, LibreOffice Impress

---

## Research Timeline & Attribution

**November 2025:** Research conducted and presentation developed independently  
**November 2025:** Presented at BSides Delaware 2025 (public conference)  
**May 2026:** Published to cornellsecurity.com as permanent research asset  

This timeline establishes **independent authorship** of the convergence framework and research prior to any formal collaborations or research partnerships.

---

## Key Resources & Standards

### NIST Standards
- **NIST SP 800-82 Rev 3** — Guide to ICS Security
- **NIST IR 8401** — Roadmap for ICS Cybersecurity Research  
- **NIST SP 800-171** — Protecting Controlled Unclassified Information

### IEEE Standards (Timing & Synchronization)
- **IEEE 1588** — Precision Time Protocol (PTP)
- **IEEE C37.118** — Synchrophasor Measurements for Power Systems
- **IEEE 802.11** — Wireless communications timing

### Industry Communities
- **Space ISAC** — Satellite security threat intelligence
- **DEF CON Aerospace Village** — Hands-on satellite security research
- **Hack-A-Sat Competition** — Satellite exploitation and defense
- **OWASP** — Application security frameworks
- **ICS-CERT** — Industrial control system advisories

---

## About the Research

**Research Focus:** Critical infrastructure security at the intersection of application security, operational technology, and signals intelligence

**Methodology:**
- Literature review of academic and industry research
- Case study analysis of real-world attacks (Viasat, Ukraine GPS warfare, UT Austin research)
- Hands-on lab validation with ICS simulation environments
- Threat modeling framework development

**Key Contributions:**
- Framework for understanding AppSec-OT-SIGINT convergence
- Case studies demonstrating real-world attack vectors
- Defense-in-depth strategy spanning four layers (RF, network, application, operational)
- Actionable guidance for defenders in critical infrastructure

---

## About the Author

**Norris P. Cornell, Jr.**  
ICS/OT Security Researcher & Author

**Background:**
- **Education:** M.S. Cybersecurity (SCADA concentration), Wilmington University, May 2022 (GPA 3.91)
- **Technical Background:** 20 years as electronics technician — provides physics-layer security perspective
- **Professional Experience:** IAM Analyst II / Core Banking Modernization Lead, Customers Bank (Nov 2021–May 2026)
- **Certifications:** CompTIA Security+ (SY0-701), FEMA IS-860.c, IS-913.a
- **Community Leadership:** Co-lead, OWASP Delaware; BSides Delaware speaker/organizer since 2015

**Research Identity:** 
Specializes in critical infrastructure vulnerabilities across physics, signals, and application layers. Focuses on the convergence of traditionally separate security domains and the hybrid attack surfaces that emerge at their intersection.

**Published Work:**
- Inputs Lie framework (4-part series on signal-layer trust failures)
- SolarWinds supply chain attack analysis
- BlackEnergy SCADA malware research
- Home lab: Proxmox + Conpot ICS simulation environment
- Research platform: Iron Gate API security validation environment

---

## Research Inquiry & Collaboration

If you're working on related research, defending critical infrastructure, or exploring the AppSec-OT-SIGINT convergence, I'm actively interested in collaborations, consulting engagements, and joint research initiatives.

**Contact:**
- **Email:** [npcornell@gmail.com](mailto:npcornell@gmail.com)
- **LinkedIn:** [Norris P. Cornell, Jr.](https://www.linkedin.com/in/norris-cornell)
- **Research Site:** [cornellsecurity.com](https://cornellsecurity.com)
- **Lab:** [Iron Gate — API Security Research](https://github.com/samson-2369/iron-gate)

---

## Copyright & Usage

© 2025–2026 Norris P. Cornell, Jr. All rights reserved.

**This research is published under the following terms:**

This presentation and accompanying materials may be viewed, downloaded, and shared for **non-commercial, educational, and professional purposes** including:
- Academic research and study
- Professional development and training
- Internal organizational use
- Conference and community presentations (with attribution)

**Prohibited uses:**
- Commercial distribution or sale without explicit written permission
- Claiming authorship or removing attribution
- Modification without consent
- Use in products or services without licensing agreement

**For licensing, consulting, or collaboration inquiries:** Contact npcornell@gmail.com

---

## Acknowledgments

This research was developed independently and draws on:
- Academic and industry research on ICS security, GNSS spoofing, and satellite communications
- Case studies of real-world incidents (Viasat, Ukraine, UT Austin research)
- Community knowledge from DEF CON Aerospace Village, Space ISAC, OWASP, and BSides Delaware
- Industry standards from NIST, IEEE, and ICS-CERT

Special thanks to the security research community for maintaining the shared knowledge that makes this work possible.

---

## Questions or Next Steps?

If this research aligns with your work or interests, reach out. I'm actively exploring research collaborations and consulting engagements in critical infrastructure security.

**Let's connect:** [npcornell@gmail.com](mailto:npcornell@gmail.com)
