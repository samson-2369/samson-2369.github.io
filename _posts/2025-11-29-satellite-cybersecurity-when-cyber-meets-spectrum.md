---
layout: post
title: "Satellite Cybersecurity: When Cyber Meets the Spectrum"
date: 2025-11-29
categories: blog
tags: [satellite SIGINT GPS-spoofing GNSS critical-infrastructure RF BSides]
excerpt: "How SIGINT, ICS, and Application Security Converge in the Invisible Domain We Depend On"
---

How SIGINT, ICS, and Application Security Converge in the Invisible Domain We Depend On

Every day, critical infrastructure runs on signals we can't see. Satellite timing guides the power grid. GNSS signals coordinate automation sequences. RF links relay data to SCADA systems. Software systems make decisions based on timing they assume is trustworthy.

Yet most cybersecurity programs treat satellites and RF systems as "someone else's problem."

I recently gave a talk at BSides Delaware 2025 making the case that this blind spot is no longer acceptable. This article expands on that research, sharing insights I hope will help defenders understand why satellite cybersecurity isn't a niche concern—it's foundational infrastructure we've been defending with our eyes closed.

The Invisible Layer We've Built Into Everything

If you pull up the architecture diagram for almost any critical infrastructure system in the United States, you'll see satellites mentioned. They're in the disaster recovery plans. They're in the facility topology. But look at the threat model, the vulnerability assessments, the incident response procedures—and they're largely absent.

This isn't because satellites aren't important. It's because we've compartmentalized them out of our mental models.

The power grid relies on GPS-disciplined clocks for synchrophasor measurements that track grid stability in real time. Wind farms use GNSS for timing coordination. Water treatment facilities depend on RF-based SCADA communications. Financial systems need atomic clock precision from satellite feeds.

Yet when we think about "critical infrastructure cybersecurity," we're still mostly thinking about firewalls, VPNs, and network segmentation.

The problem is that satellites operate in a domain your traditional security controls don't reach. Firewalls can't filter RF signals. IDS signatures don't exist for modulated waveforms. Your zero-trust architecture doesn't include the spectrum.

This is the gap we need to close.

The Attack Surface You Can't See

To understand satellite vulnerabilities, you first need to understand how traditional attacks differ from RF-layer attacks.

A traditional network attack works like this: adversary compromises a VPN, or steals credentials, or finds an unpatched service, and gains access to your environment. Your SOC has tools to detect this—firewalls log the connection, EDR catches the lateral movement, SIEM correlates the events. It's still difficult, but it's within the scope of things we've learned to defend against.

An RF-layer attack works differently.

Adversaries don't need to be inside your network. They don't need credentials or exploits. They need a software-defined radio (SDR), a few thousand dollars in equipment, knowledge of your signal structure, and physical proximity or line-of-sight to your signal source. Then they can intercept, spoof, or jam the signal—all before it becomes a packet your security controls can see.

This is signals intelligence (SIGINT) applied to critical infrastructure. And unlike traditional cybersecurity where we've been building defenses for decades, most infrastructure operators have zero visibility into this domain.

When RF Vulnerabilities Become Operational Disasters

Here's the part that keeps infrastructure security leaders awake at night: RF vulnerabilities only become operational disasters when they meet application security failures.

Let me make this concrete.

A synchrophasor protection relay receives timing information from a GPS receiver. The GPS signal provides microsecond-level precision, which the relay uses to calculate power flow angles across the grid—a critical measurement for detecting instability. The application developer didn't validate that GPS timestamp because back in the 1990s and 2000s, GPS spoofing wasn't a consideration for power systems. The hardware was assumed trustworthy.

Now imagine an adversary uses a civilian GPS spoofer to inject false timing data. The spoofed signal causes a 2-3 second timing error. This is minor from an RF perspective—a small signal manipulation. But from an application perspective, it's catastrophic.

The relay doesn't validate the timestamp bounds. It calculates a false power flow angle. The application logic interprets this as grid instability—specifically, an islanding event (unexpected grid section disconnection). The relay triggers false load shedding, automatically disconnecting generation.

The result: a 2-second RF manipulation causes utility operators to manually shed 50,000 customer loads, impacting hospitals, emergency services, and critical facilities.

This is the convergence that most defenders miss: an RF vulnerability + an application security failure = grid-scale operational impact.

It's not just an RF problem. It's not just an AppSec problem. It's both, simultaneously, in the same attack chain. And the defenses need to span both domains.

Real-World Evidence: When Theory Becomes Practice

We don't have to speculate about this. We have recent, documented examples.

GPS Spoofing Against Power Systems

Researchers at the University of Texas demonstrated, in peer-reviewed studies, that civilian-grade GPS spoofers could successfully deceive commercial synchrophasor applications. They showed timing errors that would propagate through protection logic and trigger false relays. The research wasn't theoretical—they tested it against real systems, real protocols, real applications.

The implication was clear: any electrical utility relying on GPS for critical timing, without proper input validation in the software stack, has a vulnerability that an adversary with modest resources can exploit.

The Viasat Attack and Wind Farm Blackout

The 2022 Viasat satellite attack provides a real-world confirmation of this threat.

Adversaries conducted a cyberattack on Viasat's KA-SAT satellite network, disrupting service to thousands of customers across Europe. But more significantly, it took approximately 5,800 wind turbines offline—wind farms in Ukraine and elsewhere that relied on satellite-based management and control communications.

To put this in perspective: 5,800 turbines represent roughly 11 gigawatts of generation capacity. That's equivalent to 8-10 large power plants going offline simultaneously. This wasn't a localized outage. It was grid-scale impact from a single satellite attack.

The turbines didn't fail because of a sophisticated zero-day. They failed because the infrastructure was architected with satellite links as load-bearing infrastructure.

What the Viasat incident revealed: satellites aren't optional infrastructure. They're in the critical path. And our threat models haven't caught up to that reality.

SIGINT Meets Application Security: A New Problem Space

This is where things get uncomfortable for most security teams.

Traditional SIGINT—the discipline of intercepting and analyzing electronic signals—has always been a military and intelligence domain. RF spoofing, jamming, and interception were problems for defense contractors and government agencies, not for utility operators and financial institutions.

But three trends are changing that rapidly:

First, the RF domain is becoming more accessible. Software-defined radios have democratized signal analysis. You can buy an SDR capable of analyzing and transmitting signals in the GHz range for a few hundred dollars. The technical barriers to entry are lower than they've ever been.

Second, critical infrastructure increasingly depends on wireless and satellite links for resilience. Hardened fiber is expensive and isn't always available in remote locations. Satellite links provide geographic diversity and backup connectivity. But that diversity comes at the cost of exposing your systems to the RF domain.

Third, most application security practices don't account for RF-level attacks. An input validation checklist doesn't mention "what if the GPS signal is spoofed?" A threat model doesn't include "adversary with SDR in the parking lot." Your secure coding standards don't address "validate that this timing signal isn't 6 hours in the future."

The result is a blind spot that's both conceptually large and practically dangerous.

Why Your Network Defenses Don't Reach Here

To make this real, let's map traditional network security controls to the RF-layer attack chain:

Firewall rules: They don't apply to RF signals. A firewall examines network traffic, but RF interception happens before the signal is decoded into packets.

Network encryption: Critical infrastructure systems often lack end-to-end encryption due to latency requirements or legacy compatibility. Even when encryption exists, it protects the channel, not the RF modulation itself.

Network segmentation: It's irrelevant if the attacker is bypassing the network entirely by attacking the wireless link that feeds into it.

IDS/IPS signatures: These look for known malicious patterns in network traffic. An RF spoof that's crafted to match the expected signal format won't trigger signature-based detection.

EDR and behavioral analysis: They monitor activity on endpoints and network flows. They don't see RF signals.

This is why the RF domain is an invisible layer. Your most mature security capabilities—the ones you've invested years in building—don't extend to it. An adversary can operate in the RF domain with relative impunity because you don't have visibility, detection, or response capabilities there.

Defense-in-Depth: What Defenders Can Do Now

This is where I shift from "here's the problem" to "here's what you can do about it."

Start with visibility. You can't defend what you can't see. Begin by cataloging which systems depend on RF-sourced data: GPS, GNSS, satellite communications, microwave links, RF sensors. Map these as critical dependencies in your architecture. Include them in your threat models.

Implement input validation at the application layer. This is classic AppSec, but applied to RF inputs. For timing-dependent systems: validate that timestamps are within reasonable bounds of your internal clock. Reject data that claims to be from the future or distant past. Implement rate-of-change validation—if a timestamp changes by more than expected in one update cycle, flag it as suspicious.

Add redundancy and correlation. Don't rely on a single GNSS receiver or satellite link. Correlate timing data from multiple sources. If they disagree beyond expected tolerances, alert on it. For critical systems, implement voting mechanisms where multiple independent sensors must agree before a significant action is taken.

Develop RF-domain detection capabilities. Partner with your RF engineers and spectrum management teams. Understand what normal RF activity looks like at your facilities. Implement spectrum monitoring to detect spoofing attempts or jamming.

Build resilience into operational procedures. When RF inputs fail or become suspicious, what happens? Design your systems to degrade gracefully rather than fail hard. Implement manual fallback procedures for critical operations if RF-sourced data becomes unavailable.

Educate your teams. Your SOC analysts, your application security engineers, your infrastructure operators—they likely don't think about RF attacks as part of their threat model. Build training that explains RF vulnerabilities, SIGINT concepts, and how they apply to your systems.

The Timeline Matters

If this all sounds like emerging threat theory, consider the timeline:

University of Texas research on GPS spoofing against power systems: mid-2010s

Viasat attack demonstrating grid-scale impact: 2022

SDR capabilities becoming more accessible: ongoing

Adversary capabilities and sophistication: increasing

The theory isn't emerging anymore. The threat is present. And the window for getting ahead of it is closing.

Moreover, nation-states with significant SIGINT capabilities are increasingly interested in critical infrastructure as a strategic target. They have the resources to develop RF-layer exploits. They have the intelligence to understand your specific systems, frequencies, and protocols. The sophistication bar for RF-based attacks is rising.

Making the Invisible Visible

Coming back to where we started: satellites are the invisible layer of your infrastructure. They're in your architecture diagrams. They're in your disaster recovery plans. They're woven into your most critical operational systems. But they're absent from your threat models, your security assessments, and your incident response procedures.

Making the invisible visible means:

Acknowledging the dependency — Mapping where satellite and RF-sourced data flows through your critical systems.

Extending your threat model — Adding RF-layer attacks alongside network attacks in your scenario planning.

Implementing technical controls — From input validation to redundancy to RF-domain monitoring.

Developing specialized expertise — Building internal capabilities or partnerships that bring SIGINT and RF knowledge into your security program.

Updating standards and compliance — Working with industry bodies to ensure that satellite cybersecurity becomes a recognized, required part of critical infrastructure defense.

This isn't theoretical. It's not a future-state problem. It's happening now, in systems we depend on, defended by organizations that don't yet have the tools or frameworks to address it.

What's Next

For security teams: Start with the visibility step. Catalog your RF dependencies. Include them in threat models. Begin conversations with your infrastructure operators and RF engineers about how these systems are protected.

For government and critical infrastructure agencies: This is a priority area for national security. The sophistication of potential adversaries, the grid-scale impact of successful attacks, and the immaturity of existing defenses all point to this being a strategic vulnerability.

For researchers and defenders: This is an opportunity to contribute to a domain that's still developing. RF security applied to critical infrastructure is understudied. Contributions—whether in standards development, open-source tooling, vulnerability research, or published guidance—have outsized impact.

The convergence of SIGINT, ICS, and application security is happening. The question for each organization is whether you'll make the invisible layer visible before an adversary does it for you.

Let's Connect

I'm interested in connecting with defenders, researchers, and organizations working on similar challenges in critical infrastructure security and satellite cybersecurity. If you're addressing RF-domain vulnerabilities in your organization, or you're researching this space, I'd welcome the conversation.

Comment below or reach out directly—I'm working with organizations addressing these gaps and always interested in connecting with people thinking deeply about critical infrastructure resilience.

This research and these insights come from my work at the intersection of RF security, industrial control systems, and application security. I presented this research at BSides Delaware 2025, and I'm actively working to advance the field's understanding of these threats.

The window to get ahead of this threat is still open. Let's make the invisible visible.

About the Author

I'm a cybersecurity professional with background in electrical engineering and specialized expertise in SCADA systems and critical infrastructure security. I work as a blue team defender in identity and access management, and conduct research in the intersection of RF security and application security. My focus is translating complex technical domains—whether electrical systems, RF phenomena, or satellite architecture—into actionable security insights for security teams, operators, and incident responders.

Keywords: satellite cybersecurity, SIGINT, critical infrastructure, GPS spoofing, RF security, GNSS, synchrophasor, application security, power grid security

