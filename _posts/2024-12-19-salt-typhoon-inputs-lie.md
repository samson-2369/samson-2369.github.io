---
layout: post
title: "When Valid Credentials Don't Mean \"Authorized\": What the Salt Typhoon Breach Teaches Critical Infrastructure Defenders"
date: 2024-12-19
categories: [research, threat-intelligence]
tags: [Salt-Typhoon, IAM, ICS, zero-trust, inputs-lie, critical-infrastructure, telecom]
author: Norris Cornell
excerpt: "Salt Typhoon didn't break encryption or exploit zero-days. They exploited a systemic trust assumption present across every sector of critical infrastructure: valid input equals legitimate intent."
---

*IAM | SCADA Cybersecurity — December 19, 2024*

## Executive Summary

In October 2024, U.S. authorities confirmed that Chinese state-sponsored actors—tracked as Salt Typhoon—had compromised at least nine major U.S. telecommunications providers. The breach, which persisted for over a year undetected, accessed call records from more than one million users, intercepted private communications of high-profile political figures, and compromised CALEA lawful intercept systems designed for law enforcement use.

This wasn't a sophisticated zero-day exploit. It was something more fundamental—and more dangerous.

Salt Typhoon succeeded because modern telecommunications infrastructure makes the same trust assumption that plagues industrial control systems, cloud services, and satellite networks:

**Valid input equals legitimate intent.**

This article examines what actually happened in the Salt Typhoon breach, why detection failed for so long, and what it reveals about a systemic vulnerability pattern I call "Inputs Lie"—a failure mode that extends far beyond telecommunications into every sector of critical infrastructure.

## Part 1: The Breach Nobody Saw Coming

### Timeline and Scope

**October 2024:** FBI and CISA publicly confirm PRC state-sponsored compromise of U.S. telecommunications infrastructure — undetected for over a year.

The scope of compromise included:

- At least 9 confirmed U.S. telecommunications providers including Verizon, AT&T, T-Mobile, Lumen Technologies, and others
- Call detail records (metadata) from 1+ million users
- Content interception of fewer than 100 individuals including Donald Trump, JD Vance, Harris campaign staff, and congressional personnel
- Access to CALEA lawful intercept systems
- Global reach extending to 80+ telecommunications companies across dozens of countries

By January 2025, the U.S. Treasury Department sanctioned Sichuan Juxinhe Network Technology Co., a Chinese firm identified as providing direct support to Salt Typhoon operations.

### What Made This Different

**Multi-Year Persistence:** Active presence in networks from approximately 2022-2023, discovered only in September 2024.

**Living-Off-the-Land Techniques:** Attackers used legitimate administrative tools already present in telecom environments—SSH, SNMP, Telnet, standard network management utilities. No custom malware. No exotic exploits.

**Strategic Intelligence Value:** Access to lawful intercept target lists revealed which individuals were under U.S. surveillance, allowing adversaries to identify compromised intelligence operations.

**Infrastructure Mapping:** Visibility into network topology, routing behavior, and interconnections between telecommunications providers and critical infrastructure sectors.

## Part 2: The Technical Attack Chain

### Phase 1: Initial Access via Internet-Facing Vulnerabilities

Salt Typhoon exploited known vulnerabilities in internet-facing network devices:

- **Ivanti Connect Secure VPN:** CVE-2023-46805 (Authentication bypass), CVE-2024-21887 (Command injection)
- **Cisco vulnerabilities** in router and security appliances

Telecommunications providers face unique patching challenges: 24/7 uptime requirements, complex interdependencies, vendor-specific maintenance windows, and regulatory constraints on service interruptions. These create windows where known vulnerabilities remain exploitable for extended periods.

### Phase 2: Credential Theft and Lateral Movement

Once inside, attackers focused on credential harvesting via configuration files, management protocols (SSH keys, SNMP community strings), and trust relationships between management systems. With valid credentials, lateral movement looked like routine administration.

### Phase 3: Strategic Network Visibility

With management-plane access established, Salt Typhoon gained visibility into BGP routing tables, complete network topology, and—most significantly—CALEA lawful intercept target lists.

### Phase 4: CALEA System Compromise

CALEA requires telecommunications carriers to design systems capable of supporting lawful surveillance when presented with court orders. Salt Typhoon's access to these systems meant attackers could:

1. Identify which individuals were under active surveillance
2. Access the same intercepted communications
3. Potentially modify or delete evidence of their own activities
4. Map U.S. intelligence priorities

## Part 3: Why Detection Failed

### Challenge 1: Legitimate Tools, Illegitimate Intent

Attackers used standard administrative tools already present in every telecom environment. Security monitoring systems are tuned to detect *anomalous* behavior. When attackers use legitimate tools with valid credentials, the activity appears completely normal.

### Challenge 2: Credential-Based Trust Without Continuous Verification

Telecommunications systems make a fundamental assumption:

> Valid credential + Valid protocol format = Trusted action

What systems **don't** verify:
- Is this the same device that authenticated earlier?
- Is this user in their normal geographic location?
- Does this activity match historical behavior patterns?
- Should this administrative action be happening at this time?

The credential was valid. The session was valid. The protocol format was correct. But the **intent** was malicious. This is what I call the "Inputs Lie" problem.

### Challenge 3: Management Networks as Low-Visibility Environments

Management networks, CALEA systems, and administrative infrastructure often receive less intensive monitoring because they're assumed to be "trusted" environments. Attackers operated in the least-monitored portions of the network—exactly where strategic intelligence lives.

### Challenge 4: Multi-Vendor Complexity

Detecting an attack chain that moves across Vendor A's VPN → Vendor B's router → Vendor C's management system → Vendor D's CALEA platform requires log correlation across incompatible formats, disparate timestamps, and systems that may not share the same authentication infrastructure.

## Part 4: The "Inputs Lie" Pattern Across Critical Infrastructure

| Domain | Trusted Input | Missing Verification |
|--------|--------------|---------------------|
| Telecom | Valid credentials | Device identity, behavior, timing |
| ICS/SCADA | Correct protocol format | Command source legitimacy, operational context |
| Cloud | Valid session token | Geographic consistency, device fingerprint |
| GNSS | Signal structure match | Cryptographic signal authentication |
| BGP Routing | Valid route announcement | Origin verification, path validation |

In every case: **Format compliance ≠ Trust**

## Part 5: What Defense Actually Looks Like

### Defense Layer 1: Behavioral Analytics and Anomaly Detection

- Admin account logged in from Beijing 10 minutes after accessing from Virginia → physically impossible travel
- Session token used from device never seen on the network → device fingerprinting alert
- Bulk data export from CALEA system at 3 AM Sunday → timing + volume + criticality scoring

### Defense Layer 2: Risk-Based Continuous Authentication

Shift from "authenticate once, trust for session duration" to "continuously evaluate risk and re-challenge when needed."

```
Initial Login: Username + Password + MFA
├─ Low Risk Action (view reports): No re-auth needed
├─ Medium Risk (config change): Require MFA every 30 min
└─ High Risk (CALEA access): Fresh MFA + manager approval
```

### Defense Layer 3: Device Identity and Fingerprinting

Bind authentication to specific devices via certificate-based device authentication, hardware-backed TPM verification, and device posture assessment. Even with stolen credentials, attackers can't access systems from their own infrastructure.

### Defense Layer 4: Immutable Audit Logging

Stream logs in real-time to write-once storage on a separate network segment with cryptographic verification. Even with complete network compromise, attackers can't erase evidence.

### Defense Layer 5: Zero Trust for OT/ICS

Zero Trust doesn't mean "authenticate every command." It means "trust nothing, verify everything—at the right layer." Verification happens in parallel with control commands, not inline—no latency added to control loops.

## Part 6: The Strategic Reality

When Chinese APT groups can sit undetected in telecommunications networks for 1-2 years and access lawful intercept systems, the question isn't "Can they compromise our systems?" The question is: **"When they activate those capabilities, will we detect it fast enough to respond?"**

## Part 7: The Hard Questions to Ask Your Team

1. If an attacker stole admin credentials today, how long would it take us to detect unauthorized access?
2. Can we correlate security events across our multi-vendor infrastructure?
3. Do we monitor management plane activity as intensively as customer-facing systems?
4. Can attackers with admin credentials delete or modify their own audit trails?
5. Do we re-verify user identity and intent after initial authentication?

## The Bottom Line

Salt Typhoon didn't break encryption. They didn't invent new attack vectors. They just operated inside systems that equate:

**Valid input = Legitimate intent**

That's the vulnerability. And if you're securing critical infrastructure—telecommunications, energy, water, transportation, or industrial control systems—it's probably in your environment right now.

---

*This is Part 1 of the "Inputs Lie" series examining trust failures across critical infrastructure.*

---

**Jack Cornell** is a Controls Management Specialist with nearly 20 years of electronics technician experience and a Master's degree in SCADA Cybersecurity from Wilmington University. He previously held DoD Secret clearance and has been a BSides Delaware volunteer and organizer since 2015.
