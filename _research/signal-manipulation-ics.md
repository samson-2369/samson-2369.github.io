---
layout: paper
title: "Signal Manipulation in Industrial Control Systems: Why Traditional Security Fails at the Physics Layer"
date: 2026-03-09
version: "Research Paper"
description: "How signal manipulation attacks bypass traditional ICS security controls at the physics layer — and what defenders need to do differently."
pdf: /assets/papers/signal-manipulation-ics.pdf
---

## Note on Responsible Disclosure

All signal manipulation techniques discussed in this article are drawn from publicly available academic research, industry standards, and government security guidance. The goal is to help defenders understand threats they may not have considered, not to provide attack tutorials. Where specific techniques are mentioned, citations are provided to peer-reviewed research published for defensive purposes.

## When Harmonics Become Attack Vectors

Industrial control systems are built on an assumption: that input signals follow predictable physical laws. A 4–20mA current loop should vary smoothly. A 60Hz AC waveform should be sinusoidal. A sensor reporting temperature should change gradually, not instantaneously.

But physics also gives us harmonics — integer multiples of fundamental frequencies that naturally occur in electrical systems. A 60Hz power signal generates harmonics at 120Hz, 180Hz, 240Hz, and so on. In normal operation, engineers design systems to filter out these harmonics because they represent noise or inefficiency.

Here is the security problem: most control systems validate the fundamental frequency but do not verify harmonic content. They ask "is this a 60Hz signal?" without asking "is this a clean 60Hz signal?"

## Why This Matters for Defenders

An adversary with physical or RF access does not need to compromise authentication systems or break encryption. They can inject harmonic content that:

- **Causes sensors to misreport values** — Harmonics can push analog-to-digital converters outside their expected operating range, creating measurement errors that look legitimate to downstream systems
- **Triggers protective relays prematurely** — Power systems use frequency-sensitive protection schemes. Harmonic injection can make a healthy system appear unstable
- **Bypasses signal validation** — If your ICS logic checks "signal present, frequency correct, amplitude in range," it will not detect a harmonically-distorted signal that meets all three criteria

This is not theoretical. Researchers have demonstrated harmonic injection attacks against industrial vibration sensors (causing false equipment shutdown alarms), power quality monitors (masking actual grid instabilities), and MEMS-based accelerometers used in navigation systems.

## The Detection Challenge: Why Fourier Analysis Is Not Enough

If you have an electrical engineering or signal processing background, your first instinct might be to use Fourier analysis to detect anomalous harmonic content. The mathematics are sound — a Fourier transform decomposes any signal into its constituent frequencies, revealing harmonics that should not be there.

In theory, you could establish a baseline harmonic profile for each sensor and alarm when the frequency spectrum deviates. A clean 4–20mA loop should have minimal high-frequency content. If a Fast Fourier Transform (FFT) suddenly shows significant energy at unexpected frequencies, that is your indicator of compromise.

But operational reality is more complicated:

- **Time-frequency tradeoff** — Standard Fourier analysis tells you what frequencies are present but not precisely when they occurred. An attacker could inject a 200-millisecond harmonic burst that causes a relay to trip, but your frequency analysis averaged over a 1-second window might miss it entirely.
- **Real-time constraints** — FFT is computationally efficient, but it is still computation. A SCADA system processing thousands of sensor inputs at millisecond intervals cannot afford the latency of performing frequency analysis on every signal.
- **Baseline complexity** — "Normal" harmonic content is not static. It varies with electrical load, temperature, equipment age, and operating conditions. Building an accurate baseline requires extensive data collection across all normal operating states.
- **Adversary adaptation** — A sophisticated attacker might craft signals that look clean in the frequency domain but still cause malicious effects.

The bigger problem is that most ICS environments are not even attempting Fourier analysis on sensor signals. Legacy systems were not architected for signal-level monitoring, engineering teams have electrical expertise but not security-focused signal analysis training, and nobody's threat model includes physical-layer attacks because network security consumed all the budget.

## The Trust Boundary Problem

This maps directly to OWASP A08:2021 — Software and Data Integrity Failures, but at the physical layer. Your application code might perfectly validate digital inputs, but if the sensor is receiving a manipulated analog signal, your validation happens too late in the chain.

Traditional IT security asks: "Is this data from an authenticated source?"

Physical layer security must also ask: "Does this signal's shape match what physics says it should be?"

## What Defenders Actually Need

The mathematics for detecting harmonic attacks have existed for 200 years — Fourier series is not new. What is missing is the security mindset that says defenders should be analyzing signals, not just packets.

If you are protecting critical infrastructure, your security program needs:

1. **Signal integrity monitoring** — Not necessarily full FFT on every sensor, but at minimum, anomaly detection on signal characteristics: rise time, noise floor, unexpected frequency content
2. **Multi-sensor correlation** — One sensor reporting an anomaly might be compromised. Three independent sensors should correlate. If they do not, investigate the divergence
3. **Physics-based baselines** — Machine learning models trained on what "normal" signals look like, not just normal values. A temperature reading of 72°F might be valid, but if it jumped from 65°F in 10 milliseconds, that violates physical reality
4. **Analog domain expertise** — Your ICS security team needs people who understand signal integrity, resonance, and analog circuit behavior — not just network protocols

The electronics technician in me knows this: every signal has a signature. Clean sensor data looks different from manipulated data if you know what to measure.

## Beyond Harmonics: The Broader Signal Manipulation Landscape

Harmonic injection demonstrates a fundamental principle: if you can manipulate the physical signal, you can bypass every digital security control downstream. But harmonics are just the beginning. Any measurable property of a signal — amplitude, frequency, phase, timing, modulation — becomes a potential attack vector when systems trust their inputs without verification.

### Amplitude Manipulation: Making Sensors Lie

The simplest signal attack is also the most effective: change the amplitude and the system reads a different value.

A 4–20mA current loop is the workhorse of industrial instrumentation. The current value directly represents the measured parameter — 4mA might represent 0 PSI pressure, 20mA represents 100 PSI, and everything scales linearly in between. The system reads the current and trusts that it accurately reflects reality.

The vulnerability: if an attacker can inject or attenuate current on that loop, they can make the system believe anything they want. Report 8mA when actual pressure is at 18mA, and suddenly a critically high-pressure condition looks normal. The SCADA system logs "everything fine" while physical equipment fails.

This is not exotic — it is basic circuit manipulation. But it is devastatingly effective because most systems have no way to validate that the electrical signal matches physical reality. They trust the number because the signal format is correct.

### Timing Attacks: When Nanoseconds Matter

GPS and GNSS systems are perhaps the clearest example of timing-based signal manipulation, but the principle applies anywhere precise time synchronization matters — which in critical infrastructure is nearly everywhere.

Power grids rely on synchrophasors (PMUs) to monitor grid stability across vast distances. These devices must timestamp measurements with microsecond precision to detect phase angle differences that indicate instability. If an attacker can manipulate the timing reference those PMUs use, they can make a destabilizing event invisible or create the appearance of instability where none exists.

GPS signals are extraordinarily weak by the time they reach Earth — about -130 dBm, roughly equivalent to viewing a 25-watt light bulb from 10,000 miles away. A GPS spoofer transmitting from a few hundred meters can easily overpower the authentic signal. The system receives a signal with correct structure — proper satellite IDs, valid navigation messages, appropriate signal strength — but the timing is shifted by milliseconds or microseconds. Digital validation passes. The attack succeeds.

In 2013, researchers at the University of Texas successfully spoofed the GPS aboard a superyacht, causing it to alter course without the crew realizing anything was wrong [3]. The navigation system believed its position was accurate because every technical validation succeeded — except the fundamental assumption that the GPS signal was authentic.

### Phase Manipulation: Three-Phase Power and Beyond

Three-phase electrical power systems deliver electricity using three sinusoidal voltages, each separated by 120 degrees of phase. This phase relationship is fundamental to how motors operate, how transformers work, and how power is distributed efficiently.

If you can shift the phase angle between conductors while keeping voltages and frequencies within normal ranges, you can cause motors to produce incorrect torque, create circulating currents in transformers that appear as phantom loads, and trigger protective relays that detect phase imbalance — all while each individual parameter appears within spec.

This concept extends beyond power systems. Any differential signaling scheme (RS-485, CAN bus) relies on phase relationships between signal pairs. Manipulate the phase without changing amplitude or frequency, and you can corrupt data while passing basic signal quality checks.

### Modulation Attacks: Hiding Messages in Messages

RF and telemetry systems use modulation to encode information. The attack: embed malicious modulation within legitimate modulation. The primary signal looks correct to basic demodulation, but subtle variations carry a second channel of information — or cause the receiver to misinterpret the intended message.

This is especially problematic in industrial wireless systems where spectrum is shared, interference is common, and receivers are designed to be robust rather than suspicious. A receiver that "tries hard" to decode a marginal signal might interpret attacker-controlled noise as legitimate data.

### The Unifying Theme: Trust Without Verification

All of these attacks succeed for the same reason: systems validate signal format but not signal authenticity.

- Is the signal the right frequency? ✓
- Is the amplitude within range? ✓
- Does the modulation scheme match expectations? ✓
- Is this signal actually representing physical reality? ✗

That last question almost never gets asked because it is extraordinarily difficult to answer at the speeds industrial systems operate. A protective relay cannot pause to evaluate whether a signal makes physical sense — it needs to make trip/no-trip decisions in milliseconds.

## Where Traditional Security Controls Fail

### Network Segmentation: Protecting the Wrong Boundary

Segmentation protects digital communication paths. Consider a pressure transmitter sending a 4–20mA signal to a PLC — that is an analog electrical connection over twisted-pair copper cable. There is no "network" in that signal path. No packets to filter, no IP addresses to whitelist, no TCP handshakes to inspect.

An attacker with physical access to that cable can tap the line and inject false signals, attenuate the existing signal, or introduce noise — and the firewall logs nothing, because the attack is not on the network.

You can have perfect network segmentation — air-gapped control systems, hardware firewalls, unidirectional gateways — and still be completely vulnerable to an attacker with a wire tap and basic electronics knowledge.

### Authentication: Trusting Verified Sources That Trust Unverified Inputs

Authentication answers: "Is this message from an authorized source?" It does not answer: "Is the information in this message accurate?"

Here is the attack path: a legitimate sensor is authenticated to the SCADA system. An attacker manipulates the input signal to that sensor. The sensor faithfully reports the false value using its valid credentials. The SCADA system receives an authenticated message from a trusted source — reporting false data.

Authentication succeeded. The attack succeeded.

Authentication happens after signal interpretation. By the time the system asks "who sent this?" it has already converted a manipulated analog signal into a digital value.

### Encryption: Protecting Data That Is Already Wrong

Encryption protects the confidentiality and integrity of data while it is being transmitted digitally. It does not protect the accuracy of data before it enters the digital domain.

Trace the path of a temperature reading: physical reality is 180°F. An attacker injects a voltage offset on the thermocouple leads. The sensor reads 150°F. That value is digitized, protocol-encoded, encrypted with TLS, transmitted, decrypted, and logged — perfectly securely. The attack occurred at step two.

You have built a perfect armored transport for cargo that was swapped before it was loaded.

### Intrusion Detection: Looking for the Wrong Signatures

During a timing attack on grid synchrophasors, the IDS sees: PMU sending timestamped measurements at 30 samples/second using IEEE C37.118 protocol — identical to normal operation. The timestamps are wrong because the GPS time reference was spoofed, but the IDS has no ground truth to compare against.

Signal manipulation creates no network anomalies because it does not occur on the network.

### The Air Gap Illusion

Air gaps significantly raise the difficulty of remote network intrusion, but an air-gapped control system still has sensor cables, power feeds, radio telemetry links, and GPS antennas. Every physical connection is a potential attack vector. The air gap protected the network boundary while leaving the signal boundary completely exposed.

In some ways, air-gapped systems may be more vulnerable because organizations become complacent — "we're air-gapped, so we're secure" — while an attacker only needs access to a remote junction box or utility pedestal.

## Why Security Vendors Have Not Solved This

Several factors slow progress at the physics layer:

1. **Market maturity mismatch** — The ICS security market has spent 20 years catching up to IT security basics. Many environments are still struggling with network segmentation and basic authentication. The market is not ready to pay for physics-layer security when Layer 3 is not yet solved.
2. **Deployment complexity** — Network security products sit on SPAN ports. Signal integrity monitoring requires instrumentation at every sensor — potentially thousands of devices. The installation cost is an order of magnitude higher.
3. **Expertise gap** — Building signal integrity security products requires cybersecurity expertise plus electrical engineering, signal processing, and deep domain knowledge of specific industrial processes. That combination is rare.
4. **False positive problem** — Signal-level anomaly detection faces hard challenges because "normal" signal characteristics vary with temperature, humidity, electrical load, and equipment age [6]. A product generating hundreds of false alarms per day will not survive in an operational environment.
5. **Lack of ROI visibility** — Signal manipulation attacks often look like equipment failures or operator errors [17]. Without visible incidents driving demand, there is limited incentive to invest in these capabilities.

## The Fundamental Assumption Gap

All traditional security controls share a common assumption: that inputs from physical sensors and time references represent ground truth.

- Firewalls assume that if a device is on the correct network segment, its data is trustworthy
- Authentication assumes that verified devices produce accurate information
- Encryption assumes the data being encrypted is correct
- IDS assumes that protocol-compliant traffic contains legitimate values

None of these assumptions hold when the physical layer is compromised.

IT security operates in a domain where inputs are discrete and well-defined. OT security operates in a domain where inputs are interpretations of continuous physical phenomena — and the interpretation process itself can be manipulated.

You cannot digitally authenticate an analog signal. You cannot encrypt a voltage to verify its accuracy. You cannot firewall a wire.

The security controls we have built are necessary but not sufficient. They protect against the attacks they were designed to prevent. They do not protect against manipulation of the physical signals that systems use to perceive reality.

## References

[1] National Institute of Standards and Technology. (2023). *Guide to Operational Technology (OT) Security: NIST Special Publication 800-82 Revision 3.* https://csrc.nist.gov/publications/detail/sp/800-82/rev-3/final

[2] CISA Cybersecurity & Infrastructure Security Agency. *ICS-CERT Advisory Database.* https://www.cisa.gov/ics-cert-advisories

[3] Shepard, D. P., et al. (2012). "Evaluation of the Vulnerability of Phasor Measurement Units to GPS Spoofing Attacks." *International Journal of Critical Infrastructure Protection*, Vol 6, Issue 3-4, pp. 146–153.

[4] Scott, L. (2003). "Practical Cryptographic Civil GPS Signal Authentication." *Navigation: Journal of the Institute of Navigation*, Vol. 50, No. 1.

[5] Wesson, K. D., et al. (2013). "GPS Spoofing Detection via Dual-Receiver Correlation of Military Signals." *IEEE Transactions on Aerospace and Electronic Systems*, Vol. 49, No. 4.

[6] Amin, S., et al. (2009). "Analytic Models for Sensor Attack Detection." *IEEE International Conference on Technologies for Homeland Security.*

[7] Byres, E., Lowe, J. "Physical Layer Security for Industrial Control Systems." Tofino Security. White paper.

[8] Son, Y., et al. (2015). "Rocking Drones with Intentional Sound Noise on Gyroscopic Sensors." *USENIX Security Symposium.*

[9] Hossain-McKenzie, S., et al. (2017). "Analysis of Synchrophasor Data under GPS Spoofing and Jamming Attacks." Sandia National Laboratories. *IEEE PES General Meeting.*

[10] IEEE Standards Association. (2011). *IEEE Standard C37.118.2-2011: IEEE Standard for Synchrophasor Data Transfer for Power Systems.*

[11] IEEE Standards Association. (2022). *IEEE Standard 519-2022: IEEE Standard for Harmonic Control in Electric Power Systems.*

[12] Igure, V. M., et al. (2006). "A Survey of SCADA System Vulnerabilities." *ACM Computing Surveys*, Vol. 38, No. 1.

[13] Stamp, J., et al. (2003). "Security Issues in SCADA Networks." *Computers & Security*, Vol. 22, No. 6.

[14] Brigham, E. O. (1988). *The Fast Fourier Transform and Its Applications.* Prentice Hall.

[15] National Institute of Standards and Technology. *NIST Cybersecurity Framework.* https://www.nist.gov/cyberframework

[16] Guri, M., et al. (2017). "Bridging Air Gaps Using the Electromagnetic Emanations from USB Devices." *IEEE Transactions on Information Forensics and Security*, Vol. 12, No. 8.

[17] Langner, R. (2011–2013). "Operational Technology Network Security: Lessons from Stuxnet." Various industry publications.

[18] International Electrotechnical Commission. *IEC 62443 Series: Industrial Communication Networks — Network and System Security.*

## About the Author

Norris Cornell is an Identity and Access Management professional and Technical Lead in the financial sector, where he manages IAM and PCI DSS compliance during a core banking system modernization. With nearly 20 years of electronics technician experience, he brings a distinctive perspective on the convergence of RF/SIGINT, ICS/OT security, and cyber-physical systems.

He holds a Master of Science in SCADA Cybersecurity and has been a volunteer, organizer, and speaker at BSides Delaware since 2015, most recently presenting "When Cyber Meets the Spectrum" at BSides Delaware 2025 on satellite cybersecurity and critical infrastructure protection.

Norris operates CornellSecurity.com as a cybersecurity research platform. His research focuses on helping defenders understand physics-layer security threats in critical infrastructure environments.
