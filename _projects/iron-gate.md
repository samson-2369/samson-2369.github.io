---
layout: default
title: "Iron Gate: API Security Detection Lab"
description: "Hands-on security research lab demonstrating API attack detection in OT-adjacent environments"
date: 2026-05-20
category: research
tags: [API Security, OT, ICS, Detection, SCADA]
permalink: /projects/iron-gate/
---

# Iron Gate: API Security Detection Lab

A hands-on security research lab demonstrating API attack surfaces and detection techniques in operational technology (OT)-adjacent environments.

## Overview

Iron Gate is the practical foundation for [*Inputs Lie Part 4: Detection at the Signal Layer*](/research/inputs-lie-part-4-detecting-lies-at-the-signal-layer/). The lab demonstrates how defenders can detect API-layer attacks when logging is incomplete, timing-based evasion is deployed, and traditional detection windows fail.

## Architecture

- **crAPI (OWASP Vulnerable API)** on Ubuntu 22.04 with Grafana + Loki detection stack
- **Conpot ICS Honeypot** simulating Modbus, Siemens S7, BACnet protocols
- **Attacker VM (Kali 2026.1)** for executing OWASP API Top 10 attack scenarios
- **Monitoring Stack** with Grafana dashboards and Loki alert rules

## Lab Findings

### Finding 1: BOLA Enumeration Detection
- **Attack:** 200 requests against `GET /workshop/api/shop/orders/{id}`
- **Result:** 5 HTTP 200s buried in 195 HTTP 500s
- **Detection:** Sequence clustering + behavioral anomaly detection catches what request-level rules miss

### Finding 2: Timing Drift Evasion
- **Attack:** Request spacing at 4-minute intervals
- **Result:** Evades 5-minute detection window entirely
- **Defense:** Sliding windows + exponential backoff detection required

### Finding 3: Logging Blind Spot (Fixed)
- **Problem:** Django debug logs lacked HTTP status codes
- **Result:** Broken-auth rule never fired across 6 attack sessions
- **Fix:** nginx reverse proxy with structured JSON logging + Loki rules
- **Outcome:** Attacker IP (10.0.0.101) captured and attributed

## Connection to Research

These findings validate detection techniques published in [*Inputs Lie Part 4*](/research/inputs-lie-part-4-detecting-lies-at-the-signal-layer/). The lab demonstrates Techniques 1–4 using real attack scenarios against crAPI (API layer) and Conpot (OT layer simulator).

## GitHub Repository

Full source code, Ansible playbooks, and lab setup instructions available at:

**[github.com/samson-2369/iron-gate](https://github.com/samson-2369/iron-gate)**

All findings, attack parameters, and detection rules are documented for reproducibility.

## Methodology

All attacks executed in controlled Proxmox lab environment. Attack parameters (request count, timing, payloads) documented per session to enable reproducible testing.

For detection methodology and full analysis, see [*Inputs Lie Part 4: Detection at the Signal Layer*](/research/inputs-lie-part-4-detecting-lies-at-the-signal-layer/).
