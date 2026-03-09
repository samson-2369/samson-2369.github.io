---
layout: post
title: "The Water Sector's Default Password Problem"
date: 2025-12-16
categories: blog
tags: [water-sector ICS OT Aliquippa inputs-lie authentication]
excerpt: "November 25, 2023. A remote booster station serving 6,000 people in Pennsylvania was accessed by a hostile actor. The international media followed. Defacement banners appeared on the HMI. Operators we"
---

November 25, 2023. A remote booster station serving 6,000 people in Pennsylvania was accessed by a hostile actor. The international media followed. Defacement banners appeared on the HMI. Operators were forced to switch to manual operation.

Here's what didn't happen: No zero-day. No exploit chain. No malware. No sophistication.

A publicly available default password. Shodan scanning. Transparent trust in factory credentials.

This is Aliquippa. And it's the perfect example of the Inputs Lie framework applied to critical infrastructure.

Before You Read This: What You're Looking At

I've spent nearly twenty years as an electronics technician before moving into cybersecurity. In that time, I learned something that OWASP documents later: sensors lie, signals drift, and if a system trusts bad input, it fails. Sometimes violently.

What happened at Aliquippa wasn't new. It was the exact failure mode I'd seen in embedded systems for decades, just moved into operational technology with higher stakes.

This analysis isn't about sophisticated attacks. It's about predictable failures from unchanged assumptions. If you work in OT security, compliance, or critical infrastructure — this should anger you. Because these failures are entirely preventable.

The Aliquippa Incident: Anatomy of Negligence

CyberAv3ngers (assessed to be Iranian IRGC-affiliated) began a coordinated campaign against water utilities in late 2023. The scope tells you everything: 75+ compromised devices across 34 U.S. water and wastewater facilities. Additional hits in the UK. A 48-hour outage in Ireland affecting 180 customers.

Attack restraint masked organizational negligence. Most incidents stopped at defacement. But the attackers had full access. They could have manipulated process setpoints, altered tank levels, disabled alarms. They didn't. That's not a sign of resilience. That's a sign of attacker restraint.

And from a defensive perspective? That distinction is useless. You can't plan your security around hoping adversaries are nice.

The Attack Chain: Embarrassingly Simple

Step 1: Internet Scanning

Attackers used Shodan to identify internet-exposed Unitronics PLCs. Distinctive service banners, open management ports, predictable fingerprints. Finding them is trivial. As of 2024, more than 1,700 Unitronics PLCs sit on Shodan — many still sporting factory credentials and public internet access.

Step 2: Default Credentials

Factory defaults are documented in publicly available vendor manuals. No brute-forcing. No exploitation. No clever bypasses. Attackers tried the well-known credentials. Authentication succeeded. The system did exactly what it was designed to do: grant full trust after login.

Step 3: HMI Access and Control

Authenticated, the attackers gained access to the human-machine interface and management functions. They modified display text, read real-time process values, could interact with control functions. The defacement wasn't evidence of compromise. It was evidence of complete trust after authentication.

Why This Works: Decades-Old Design Choices

Unitronics PLCs use proprietary protocols over TCP/IP. They were never designed for this world.

No encryption on management traffic. Credentials transmitted in plaintext. Minimal session management. No cryptographic authentication. No integrity checking. These design choices made perfect sense when PLCs lived in isolated, physically secured networks.

But that was decades ago. And those assumptions didn't age well once the internet showed up.

This is Inputs Lie

Here's the pattern: Systems implicitly trust external inputs—credentials, commands, signals, data—because they were designed for cooperative environments, not adversarial ones.

Watch the layers break down in Aliquippa:

The PLC trusts factory defaults remain safe. Successful authentication proves legitimacy even though the credentials are publicly known. The utility trusts vendor reputation and legacy practices over continuous validation. Internet exposure is treated as benign because it's convenient. At every layer—trust replaces verification.

This is the problem. Not the nation-state. Not the APT. The problem is infrastructure built on implicit trust that never should have been implicit.

From AppSec to OT: Same Failure, Different Domain

For application security folks, this maps to OWASP A07: Identification and Authentication Failures. But the parallels run deeper than just category mapping.

In AppSec, A07 shows up as default credentials, weak authentication, no MFA, over-privileged accounts. Applications shipped configured to fail open.

In ICS, same thing. PLCs ship with defaults enabled. Password changes get deferred to "avoid disruption." Authentication is single-factor. Successful login grants broad system trust.

The difference? In ICS, authentication failure isn't a database breach. It's a tank rupture. A pressure vessel exceeding limits. Physical safety incidents. The consequence isn't compromised data. It's compromised physics.

This Isn't Unique to Water. Or ICS. Or Anything.

GNSS spoofing exploits trust in unauthenticated navigation signals. Supply chain attacks exploit trust in update mechanisms. Social engineering exploits trust in caller authority. API attacks exploit trust in unvalidated tokens.

Across every domain, the pattern holds: systems accept inputs at face value because when the inputs were designed, deception wasn't part of the threat model.

This convergence tells you something uncomfortable. The vulnerability isn't domain-specific. It's fundamental to how we design systems. Add security later. Add validation later. Add mistrust later. The result is always predictable.

The Mitigations (They Exist. They're Cheap.)

Zero Cost

Change all default credentials. Disable unnecessary remote access. Restrict management interfaces to internal networks only. Enable device logging. Maintain an asset inventory. These aren't optional. They're operational hygiene.

Trivial Cost

VPN-based remote access. Network segmentation with VLANs and zones. Open-source SIEM platforms for centralized logging. Credential rotation and access reviews. None of this breaks the bank. CISA, NIST SP 800-82, and AWWA have all documented this guidance.

The Cost of Failure

Incident response and forensics: $50K to $500K. PLC replacement: $10K to $100K per device. Service disruption: $1M+ per incident. Loss of public trust: immeasurable. Against those numbers, basic security controls represent trivial investment. And yet organizations still skip it.

The Real Problem Isn't Technical

From a national security perspective, these incidents show how nation-state actors pre-position themselves within critical infrastructure by exploiting basic negligence. This isn't a technology problem. This is governance and culture.

As long as OT security stays regulation-driven instead of threat-driven, adversaries will exploit the gap between compliance theater and actual security. You can check all the boxes, pass all the audits, and still hand your infrastructure to the first attacker who tries a Shodan search.

The tools exist. The mitigations are documented. The cost is negligible. What's missing is willingness. Willingness to challenge why you're still trusting factory defaults. Willingness to assume credentials can leak. Willingness to verify instead of trust.

The Question Isn't "Can We Prevent This?". We Can.

The question is whether your organization will act before the next intrusion escalates from defacement to physical harm. Because Aliquippa happened at an attacker's discretion. Next time, you might not be dealing with tactical restraint.

Inputs Lie. Systems trust what they shouldn't. And until we replace implicit trust with continuous verification, we're all just waiting for the next CyberAv3ngers campaign to remind us what we already knew.

