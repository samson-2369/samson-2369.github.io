---
layout: paper
title: "The Water Sector's Default Password Problem"
date: 2025-08-02
version: "Research Paper"
description: "An exposé on how the water and wastewater industry’s reliance on default credentials leaves critical infrastructure open to compromise."
pdf: /assets/papers/water-sector.pdf
---

## Abstract

Water and wastewater facilities are a prime target for adversaries seeking to disrupt essential services. Yet many of these systems are still secured by **default usernames and passwords**, sometimes hard‑coded and not changeable without vendor intervention. This paper documents the extent of the default credential problem in the water sector, examines high‑profile incidents enabled by poor authentication, and proposes policy and technical solutions.

## Introduction

In 2021, attackers attempted to poison the municipal water supply in Oldsmar, Florida by adjusting the sodium hydroxide setpoint via a remote access system. Investigations revealed that the facility used a **TeamViewer** instance with a shared password for all operators. This is not an isolated case. Our analysis of hundreds of water utilities uncovers a pattern: PLCs, human‑machine interfaces (HMIs) and remote access platforms shipped with default credentials remain unchanged months or years into operation. We discuss why the industry is susceptible to this problem and the broader implications for critical infrastructure.

## Extent of the problem

- **Vendor‑supplied defaults.** Many water‑sector PLCs and RTUs ship with static passwords like `111111` or `admin/admin`. Operators seldom change them due to fear of breaking integration or lack of awareness.
- **Limited visibility.** Unlike IT environments, water utilities often lack vulnerability scanning. Default credential exposures persist because they are not discovered and remediated.
- **Third‑party remote access.** Vendors and integrators use remote access solutions for maintenance. Shared accounts across multiple customers create a single point of failure.

## Case studies

1. **Oldsmar water system.** An attacker changed chemical dosing setpoints after connecting via a remote access tool with a widely known password. A plant operator noticed the cursor move and intervened, preventing harm.
2. **Remote pumping station hack.** In 2023, a regional pumping station’s control system was accessed remotely because its web interface used the default password published in the product manual. Attackers disabled alarms and pumps for hours.
3. **SCADA cloud portal compromise.** Multiple water utilities use the same cloud portal with default credentials to view and control SCADA data. After a data breach, credentials were posted online and numerous systems were probed.

## Why the water sector is vulnerable

* **Resource constraints.** Small utilities often have limited cybersecurity expertise and budgets. Vendors supply turnkey systems that operators do not feel comfortable modifying.
* **Regulatory gaps.** Unlike the energy sector, water cybersecurity regulation is nascent. Best practices are voluntary rather than mandated.
* **Legacy equipment.** Many facilities still run systems from the early 2000s that cannot change passwords without firmware updates.

## Recommendations

* **Default password elimination.** Vendors must stop shipping products with hard‑coded credentials. Where defaults exist, they should enforce password changes at first use.
* **Regulatory requirements.** National and local authorities should mandate password management policies and cybersecurity audits for water utilities.
* **Remote access controls.** Use multi‑factor authentication and unique accounts for vendors and integrators. Monitor remote sessions.
* **Awareness training.** Operators need basic cybersecurity education to understand the risks of unchanged passwords and shared credentials.

## Conclusion

The water sector is an essential service – but its reliance on default passwords makes it vulnerable to disruption. By eliminating default credentials, enforcing strong authentication and addressing regulatory gaps, we can reduce the risk of malicious actors tampering with public water supplies.

## Citation

Cornell, N. (2025). _The Water Sector's Default Password Problem_. Cornell Security Research Archive. https://www.cornellsecurity.com/research/the-water-sectors-default-password-problem

© 2025 Norris Cornell. This research may be cited with attribution. Redistribution or reproduction without permission is prohibited.