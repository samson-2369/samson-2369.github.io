---
layout: post
title: "Asset Visibility in OT Environments: Why You Can't Defend What You Don't See"
date: 2025-08-02
categories: blog
tags: [ICS OT asset-visibility MITRE-ATT&CK Dragos Claroty]
excerpt: "When it comes to securing Operational Technology (OT) and Industrial Control Systems (ICS), visibility isn’t just nice to have—it’s non-negotiable. If you don’t know what assets exist on your industri"
---

Asset Visibility in OT Environments: Why You Can’t Defend What You Don’t See

When it comes to securing Operational Technology (OT) and Industrial Control Systems (ICS), visibility isn’t just nice to have—it’s non-negotiable. If you don’t know what assets exist on your industrial network, you can’t protect them. You can’t patch them. You can’t monitor their behavior. And most critically, you can’t detect when something goes wrong.

Asset visibility is the bedrock of any effective ICS cybersecurity strategy. Yet, in many critical infrastructure environments, it remains one of the most overlooked and underdeveloped components of cyber hygiene. This post explores why asset visibility is so challenging in OT, how to implement it safely, and the tools and frameworks that can help.

The Visibility Gap in Industrial Networks

Traditional IT environments typically have robust visibility. From asset management platforms to endpoint detection agents, most organizations have some degree of insight into what’s on their networks. OT environments are a different story.

Industrial networks often consist of decades-old systems, proprietary protocols, and “flat” architectures with little to no segmentation. Many assets—like programmable logic controllers (PLCs), human-machine interfaces (HMIs), and data historians—were never designed with cybersecurity in mind. They often lack logging, encryption, and even basic authentication mechanisms.

Why is asset discovery difficult in OT?

- Active scanning is risky: Conventional tools like Nmap or Nessus can crash fragile devices.
- Proprietary protocols: Vendors use unique communication standards, making deep inspection hard.
- Air-gapped assumptions: Many environments still operate under the illusion of isolation.
- Lack of inventory discipline: New devices get added without documentation or centralized oversight.
The Colonial Pipeline ransomware attack in 2021 serves as a high-profile example of how dangerous poor asset visibility can be. In this incident, attackers gained access to Colonial Pipeline’s IT network using a compromised VPN password for an unused account that lacked multifactor authentication. Although the ransomware did not spread into OT systems, the company made the decision to shut down its entire pipeline operation out of caution and uncertainty—highlighting a major lack of confidence in their visibility and segmentation between IT and OT networks.

The shutdown led to widespread fuel shortages and price spikes along the East Coast, demonstrating how a cyber incident in the business network can cascade into massive real-world consequences when visibility is incomplete. This case illustrates that without full awareness of what systems are connected, and how they communicate, even organizations in critical infrastructure sectors may be left in the dark when it matters most.

Passive Discovery Tools and Techniques

To gain visibility without disrupting operations, passive monitoring is the gold standard for OT environments. Instead of probing devices directly, these tools listen to network traffic, identify devices and protocols in use, and build a picture of the environment over time.

Recommended tools include:

- Nozomi Networks, Claroty, and Dragos – purpose-built for industrial visibility and threat detection.
- Zeek (formerly Bro) – a powerful passive network analyzer, with some ICS protocol support via plugins.
- Arkime – a packet capture tool that allows in-depth network traffic inspection.
- Wireshark – for protocol-level packet analysis, including Modbus, DNP3, and OPC-UA.
How it works:

- Configure SPAN ports, TAPs, or mirror ports on industrial switches.
- Feed mirrored traffic to passive sensors or a dedicated collection server.
- Tools parse traffic and fingerprint devices by IP, MAC, vendor, protocol, and firmware version.
This method allows you to build a dynamic, evolving asset inventory without touching the endpoints themselves.

Building and Maintaining an OT Asset Inventory

Discovery is just the start. To be useful for cyber defense, visibility must translate into a structured and up-to-date asset inventory.

Best practices include:

- Tag criticality: Classify assets based on their impact on safety, operations, or business continuity.
- Track firmware and software versions: Essential for identifying vulnerable components.
- Use CMDBs or EAM systems: Centralize your data so that it can feed into risk management and SOC workflows.
- Automate updates: Where possible, sync passive discovery data into your inventory system regularly.
Frameworks like the NIST Cybersecurity Framework (CSF) emphasize this in the Identify function. You can’t protect what you haven’t identified.

Detecting and Responding to Rogue or Undocumented Devices

Even with a solid asset inventory, you must remain alert for changes—especially unexpected or unauthorized ones.

Threat actors may attempt to:

- Introduce rogue engineering laptops.
- Exploit unmanaged network ports.
- Connect devices like Raspberry Pis to intercept or relay traffic.
Detection techniques:

- Establish a communication baseline for known-good traffic patterns.
- Use passive tools to alert on new MAC addresses, unusual protocol use, or port scans.
- Ingest logs into a SIEM like Splunk or Elastic to correlate and investigate anomalies.
- Map potential tactics to frameworks like MITRE ATT&CK for ICS (e.g., T0809: Rogue Master).
By continuously monitoring for deviation, you turn passive discovery into a proactive defense mechanism.

Conclusion: Visibility Is the First Step Toward Control

In ICS and OT environments, asset visibility isn’t a one-time project—it’s a continuous process that forms the foundation of every other security initiative. Without it, segmentation is blind, threat detection is unreliable, and incident response is incomplete.

If your organization is still operating in the dark, the time to act is now. Start with passive discovery, build an inventory, and continuously monitor for change.

You can’t defend what you don’t see—but once you do see it, you can take meaningful, risk-based action.


> 💬 Want to share your experience with ICS asset visibility? Let’s discuss it in the comments or connect on LinkedIn: https://www.linkedin.com/in/norriscornell
