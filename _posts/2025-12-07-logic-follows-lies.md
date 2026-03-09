---
layout: post
title: "Logic Follows Lies: How PLCs and RTUs Fail Under Adversarial Conditions"
date: 2025-12-07
categories: blog
tags: [inputs-lie PLC RTU ICS signal-manipulation]
excerpt: "A PLC or RTU accepts whatever value reaches its input buffers and applies deterministic logic to it with absolute confidence. And when those upstream signals are manipulated—whether sensor readings, t"
---

If inputs lie, logic will follow.

Industrial control systems don't reason.

They don't question.

They don't validate truth.

They evaluate.

A PLC or RTU accepts whatever value reaches its input buffers and applies deterministic logic to it with absolute confidence. And when those upstream signals are manipulated—whether sensor readings, timing references, or permissive bits—the controller's logic becomes the attack surface.

In Part 2 of this series (building on my BSides Delaware presentation), we explored how industrial systems trust external signals that were never designed for contested environments: GNSS timing, power system telemetry, and navigation signals with no integrity controls.

Now, in Part 3, we move downstream—into the controller itself—to expose why a single falsified input can trigger state transitions, bypass interlocks, destabilize PID loops, or issue dangerous physical commands.

This is how industrial logic fails under adversarial conditions.

Why PLC Logic Is Fragile When Inputs Are Manipulated

PLCs operate on a small set of truths:

•       If a rung condition is met → evaluate the next instruction.

•       If a permissive is true → enable the sequence.

•       If a timer expires → advance to the next state.

•       If a process value crosses a threshold → activate the output.

Notice what's missing:

There is no truth verification inside the controller.

A PLC does not ask:

•       "Does this value make physical sense?"

•       "Is this sensor behaving consistently with others?"

•       "Did this input change too quickly to be real?"

It simply evaluates the data it is given—and therein lies every signal-layer attack vector.

This is the foundation of every ICS spoofing attack:

A manipulated input becomes a manipulated state.

And the controller reacts with deterministic certainty—even if the reaction is hazardous.

Three Failure Modes When Inputs Are Manipulated

These failure modes appear consistently across ICS, OT, and grid environments when adversaries target the signal layer.

Failure Mode #1: Forced State Transitions

A spoofed sensor value crosses a threshold that the physical system never reached.

Examples:

•       A falsified temperature reading drops from 180°F to 85°F → PLC turns the heater on, overheating the process.

•       A manipulated tank sensor indicates "low level" → pump starts, causing cavitation or dry-run damage.

•       A falsified pressure signal shows "safe" → safety interlock is bypassed, allowing a dangerous sequence to initiate.

One manipulated value changes the state machine.

No alarms trigger—because every downstream rung evaluates normally.

Failure Mode #2: Logic Pollution

This is the most underrated ICS attack class.

An attacker changes:

•       A bit

•       A counter

•       A mode flag

•       A timer preset

•       A permissive value

... upstream of the controller.

Downstream logic processes the polluted value through:

•       Latching coils

•       Safety rails

•       Step sequences

•       PID controllers

•       Startup interlocks

The corrupted value propagates like a toxin, and every evaluation after that becomes suspect.

This is not a single control failure—this is logical corruption.

Failure Mode #3: Timing Desynchronization

Timing attacks are the silent killers of industrial logic.

Most ICS environments rely on GNSS or NTP for:

•       Synchrophasor alignment

•       Breaker coordination

•       Relay comparison logic

•       Event sequencing

•       Historian and SOE logs

•       Protection logic ordering

When an attacker spoofs or shifts timing, no malware is needed.

No firmware modification.

No protocol injection.

The system is simply confused.

Relays misfire.

Interlocks expire too early or too late.

Controllers advance steps out of order.

The system still "runs"—but not safely.

Real-World Attack Scenarios

Scenario 1: RTU Desynchronization → Breaker Trips at the Wrong Time

Grid protection relays depend on tightly synchronized phasors.

Spoof GNSS timing and you poison the foundation of grid coordination.

Impacts:

•       False breaker openings

•       Failure to trip when needed

•       Out-of-phase switching

•       Incorrect relay comparisons

•       Protection misalignment across substations

A few microseconds of timing drift can cascade into a grid event.

Scenario 2: Forced Permissive → Safety Interlock Bypassed

Safety sequences rely on permissives:

•       Tank must be full

•       Valve must be closed

•       Pressure must be stable

•       Temperature must be within range

If an attacker flips one bit, the PLC sees a safe condition that does not exist.

The controller proceeds with:

•       Startup

•       Shutdown

•       Heating

•       Chemical dosing

•       Pressurization

•       Mechanical actuation

... with complete confidence.

Scenario 3: PID Loop Instability Through Sensor Drift

PID loops trust input values completely.

If the attacker gradually spoofs a sensor:

•       The loop tries to correct a problem that isn't there

•       Outputs oscillate

•       Actuators hunt

•       Processes destabilize

•       Equipment is stressed or damaged

The system fails slowly, silently, and mathematically.

This is one of the most dangerous ICS attack patterns because operators often interpret the instability as a mechanical issue, not an adversarial one.

Why Defenders Miss These Attack Paths

Most ICS security programs focus on:

•       Patch management

•       Firmware integrity

•       Secure configuration

•       Network segmentation

•       Logging and monitoring

•       Protocol inspection

•       Firewalls and allowlists

These are necessary—but not sufficient.

Traditional security frameworks treat the signal layer as:

"Trusted infrastructure, not an attack surface."

So defenders focus on the network layer, the controller layer, and the HMI layer—but not the most manipulable layer of all:

The inputs themselves.

And because ICS logic reacts deterministically to falsified data, the attacker doesn't need to exploit the controller—they just need to lie convincingly.

Why This Problem Is So Fundamental

Because the control system is not the victim.

Reality is the victim.

When attackers manipulate inputs:

•       The PLC is not hacked

•       The RTU is not compromised

•       The HMI is not infected

•       The historian is not altered

The process is manipulated through logic behaving exactly as designed.

This is what makes signal-layer attacks so effective—and so hard to defend against.

How to Detect Logic-Level Lies (Preview of Part 4)

In Part 4, we'll explore detection strategies that most industrial security programs overlook—techniques that reveal the gap between perceived state and physical reality:

1.    Physics-Based Anomaly Detection

2.    Sensor Redundancy & Signal Correlation

3.    Timing Drift Detection

4.    State-Machine Integrity Monitoring

5.    Scan-Cycle Stability Monitoring

Each technique gives defenders visibility into the "truth layer"—the gap between what the controller sees and what the process actually is.

Closing Thoughts

Every industrial cyberattack begins with the same principle:

"If you can control what the system sees, you can control what it does."

PLCs and RTUs don't validate truth—they only evaluate inputs.

This makes the signal layer one of the easiest, most cost-effective targets for adversaries, yet one of the least defended.

In an era where operational environments are increasingly contested, defenders must stop treating sensors, permissives, and external timing as trusted infrastructure.

Because logic follows lies.

And in ICS environments, lies can break the physical world.

Want to go deeper?

Part 4 of this series will focus on the physics, timing, and redundancy techniques that detect falsified inputs—before logic fails.

If you work in:

•       Grid protection

•       Pipeline control

•       Water and wastewater

•       Manufacturing automation

•       Chemical processing

•       SCADA/ICS engineering

... I'd love to hear what detection challenges you face in your environment.

