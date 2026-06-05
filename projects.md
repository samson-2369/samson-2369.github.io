---
title: Projects
permalink: /projects/
layout: default
description: Portfolio projects and cyber defense lab work by Norris Cornell.
---

# Projects

This section showcases practical cybersecurity projects and defensive lab environments that demonstrate applied skills and research interests.

## Iron Gate — API-to-OT Detection Lab

A detection engineering lab built on Proxmox combining crAPI (intentionally vulnerable API), a Conpot ICS honeypot, and a Grafana/Loki observability stack across four VMs. The lab generates OWASP API Top 10 attack scenarios — BOLA, broken authentication, SSRF-to-OT pivot — then tests whether purpose-built LogQL alerting rules catch them. Key findings: BOLA enumeration bypasses network-layer controls entirely and requires application log correlation; attacks spaced at four-minute intervals evade standard five-minute detection windows; and logging infrastructure gaps silently break detection rules upstream. The technical foundation for the [Inputs Lie Part 4](https://cornellsecurity.com/research/inputs-lie-part-4-detecting-lies-at-the-signal-layer/) research article. Full implementation — Ansible playbooks, LogQL rules, Grafana dashboards — on [GitHub](https://github.com/samson-2369/iron-gate).

## Cyber Defense Virtual Lab

A self‑contained virtual machine environment for practicing detection engineering, incident response, and malware analysis. Includes custom scripts for network discovery, log collection, and sandboxed experimentation.

## Satellite Timing Monitor

A monitoring tool that compares GPS and GNSS timing to detect spoofing or signal disruption, illustrating the importance of signal‑layer visibility for critical infrastructure.

## OT Asset Discovery Script

A Python script that scans industrial networks to identify PLCs, RTUs, and HMIs, then enriches the data with vendor information to prioritize patching and hardening.

## SCADA Risk Assessment Framework

A methodology for assessing SCADA architectures against common attack patterns, focusing on trust boundaries, default credentials, and protocol misuse.
