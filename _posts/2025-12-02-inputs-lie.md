---
layout: post
title: "Inputs Lie: Your System Trusts Signals It Shouldn't"
date: 2025-12-02
categories: blog
tags: [inputs-lie ICS OT signal-manipulation framework]
excerpt: "If you lie to an industrial system about its inputs, it will execute that lie faithfully into the physical world. No hesitation. No intuition. Just deterministic logic doing exactly what it was"
---

Inputs Lie: Your System Trusts Signals It Shouldn’t

ICS/OT Security Series — Part 1

If you lie to an industrial system about its inputs, it will execute that lie faithfully into the physical world. No hesitation. No intuition. Just deterministic logic doing exactly what it was

designed to do.

In my last post, I talked about how satellite signals—GPS, GNSS, RF—are largely undefended against spoofing and manipulation. The gap isn’t just theoretical. It lives inside your industrial control systems.

Most ICS/OT security conversations happen inside the perimeter: PLC hardening, segmentation, protocol validation. All important, and they're where the industry has focused because that’s where defenders have leverage. But these conversations start downstream—after the true beginning of every control decision. The external signals your system inherits from infrastructure designed for a different threat landscape are the real starting point.

## THE REAL STARTING POINT OF EVERY CONTROL LOOP
Before a single rung of logic executes, your system is already trusting inputs it never validated.GPS timing for relay coordination. Satellite and RF channels treated as “trusted transport.” GNSS for precise clocks. External NTP without authentication. Raw sensor telemetry from devices that cannot verify their own integrity.These signals enter the system pre-PLC. They form the foundation every decision rests on.And they were engineered for reliability—not for adversarial robustness.

## THE DIGITAL LOGIC TRUTH
PLCs and RTUs are, at their core, deterministic digital logic. They do not reason. They evaluate.If inputs are wrong, outputs are wrong. It's that simple.A corrupted GPS timing signal doesn’t “confuse” a relay—it forces a state transition.A spoofed sensor value doesn’t make an RTU hesitate—it flips a bit in a digital register.A jammed RF signal cutting command authority is functionally identical to severing a trace to a logic gate.Digital logic does not verify truth. It processes whatever arrives at its inputs.The PLC cannot distinguish a valid signal from a well-crafted lie. The HMI displays whatever the PLC believes. The operator sees the lie rendered as truth.From there, consequences cascade.

## WHY THIS GAP EXISTS
You can’t retrofit authentication into 20-year-old GPS receivers. You can’t harden GNSS synchronization without risking operational availability. Legacy ICS infrastructure was built for an era where reliability mattered more than adversarial interference.Meanwhile, attackers have evolved faster than the infrastructure did.ICS/OT security teams focus where they have visibility and control: inside the perimeter. But the signals layer lives upstream—maintained by different vendors, teams, and assumptions.This is not a failure. It is an inherited blind spot.

## DETECTION WITHOUT REPLACEMENT
The good news is that you don’t need to rip out your existing ICS hardware.Signal-layer attacks leave detectable fingerprints:• Timing correlations that drift unexpectedly• GNSS or NTP shifts that contradict physical conditions• Redundant sensors disagreeing in subtle ways• RF anomalies inconsistent with environmental patterns• Telemetry deltas that violate basic physicsThese indicators don’t require new PLCs—they require better observability.If your GNSS drift rate changes while your physical process remains stable, that's not a coincidence. It’s a signal integrity failure.

## WHAT THIS MEANS FOR YOUR INFRASTRUCTURE
If your operations rely on external signals—timing, navigation, remote commands, distributed sensing—then you are depending on inputs you may never have threat-modeled for spoofing or manipulation.This is not a gap in your security program. It's a gap in the assumptions that shaped these systems decades ago.But it can be closed.Start by asking:Where does my operation trust external signals—and what happens if those signals lie?That’s the invisible layer most defenders overlook. Let’s make it visible.

## NEXT IN THE SERIES
Part 2: “Logic Follows Lies — How PLCs and RTUs Fail Under Adversarial Conditions”

We’ll explore how deterministic logic breaks under manipulated inputs, and what modern detection strategies must account for.

