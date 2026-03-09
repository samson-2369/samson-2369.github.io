---
layout: paper
title: "Logic Follows Lies: How PLCs and RTUs Fail Under Adversarial Conditions"
date: 2025-07-19
version: "Research Paper"
description: "An investigation into how deterministic control logic behaves when fed adversarial inputs, and how to design industrial automation that degrades safely instead of catastrophically."
pdf: /assets/papers/logic-follows-lies.pdf
---

## Abstract

Programmable logic controllers (PLCs), remote terminal units (RTUs) and distributed control systems (DCS) form the backbone of industrial automation. These devices execute simple, deterministic logic at high speed, controlling motors, valves and breakers based on inputs from sensors. They are designed for reliability and predictability – but that predictability becomes a weakness when adversaries feed false inputs. This paper examines how PLC programs react to adversarial data, why naïve control logic can amplify the impact, and how engineers can design logic that fails gracefully when data integrity is compromised.

## Introduction

In previous work (_Inputs Lie_), we established that sensor inputs cannot be blindly trusted. Here we explore the consequences: **When logic follows lies, it can magnify them.** A PLC controlling a reactor might open coolant valves wider in response to a forged temperature drop, causing actual overheating. An RTU might shed load on an electrical grid because voltage readings were spoofed. We discuss experiments demonstrating these behaviours and propose resilient control strategies.

## Analysis of control logic behaviours

1. **Open-loop behaviour.** Many PLC programs simply write outputs based on the current input without historical context. Adversarial spikes cause equally abrupt actuator changes.
2. **Integral action and windup.** PID controllers accumulate error over time. A sensor offset will cause integrators to wind up, saturate outputs and overshoot when the error is corrected.
3. **Lack of cross‑checks.** PLC logic rarely cross‑checks sensor values from different parts of the system. If one temperature probe fails high but others are normal, logic may still respond only to the faulty one.

## Designing resilient logic

* **Implement hysteresis and filtering.** Smooth out small oscillations and ignore transient spikes that exceed physical plausibility.
* **Validate against multiple inputs.** Use voting schemes where multiple sensors must agree before an action is taken. Trip signals should be corroborated.
* **Rate‑limit actuator changes.** Limit how quickly outputs can change to avoid sudden swings when inputs fluctuate.
* **Monitor for sensor disagreement.** If two redundant sensors disagree, flag the system for manual investigation and switch to a safe fallback mode.
* **Incorporate context.** Control logic should consider operational states (startup, shutdown, steady‑state) and constrain actions accordingly.

## Conclusion

Industrial automation isn’t just about writing ladder logic – it’s about anticipating how that logic behaves when the information it receives is wrong. By recognising the interplay between **inputs that lie** and **logic that blindly follows**, engineers can design systems that degrade safely under adversarial conditions, protecting equipment and the public.

## Citation

Cornell, N. (2025). _Logic Follows Lies: How PLCs and RTUs Fail Under Adversarial Conditions_. Cornell Security Research Archive. https://www.cornellsecurity.com/research/logic-follows-lies-how-plcs-and-rtus-fail-under-adversarial-conditions

© 2025 Norris Cornell. This research may be cited with attribution. Redistribution or reproduction without permission is prohibited.