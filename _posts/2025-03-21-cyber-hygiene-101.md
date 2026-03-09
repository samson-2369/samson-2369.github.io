---
layout: post
title: "Cyber Hygiene 101"
date: 2025-03-21
categories: blog
tags: [cyber-hygiene NIST IAM]
excerpt: "Cyber Hygiene 101: Explore key NIST guidelines to safeguard your digital footprint and prevent costly breaches like MGM's $100 million ransomware attack. Understand why MFA, strong passwords, regular "
---

Cyber Hygiene 101: Explore key NIST guidelines to safeguard your digital footprint and prevent costly breaches like MGM's $100 million ransomware attack. Understand why MFA, strong passwords, regular updates, and secure configurations are not optional—they're vital for your cybersecurity survival.What NIST Says About Keeping Your Digital Footprint Clean

Hey there—cyber hygiene is your digital lifeline. It's the daily grind that keeps your footprint clean and hackers at bay: strong passwords, updates, and locked-down configs. Skip it, and you're begging for trouble. Just ask MGM Resorts—one cyber hygiene slip in September 2023 cost them over $100 million.

I've spent over three years working in SIEM monitoring, vulnerability management, and security hardening—triaging Splunk logs, locking down systems, and following NIST best practices. Whether securing financial systems in Region 3, near Philly or analyzing real-world breaches, one thing is clear: cyber hygiene isn't optional—it's survival.

MGM's $100M Cyber Hygiene Lesson

On September 8, 2023, ALPHV/BlackCat and Scattered Spider launched a ransomware blitz on 29 MGM properties—Bellagio, MGM Grand, you name it. ATMs crashed, slot machines failed, and digital keys stopped working for 10 days. How?

- Social Engineering: The Weakest Link – An attacker scraped an MGM employee's LinkedIn, called IT, and sweet-talked their way into an MFA reset.

Poor Identity Verification: Ten minutes later, they had admin access to Okta and Azure and stole 6+ terabytes of data—SSNs, IDs, and personal info for millions of customers.

Weak MFA & Monitoring: There are no advanced authentication checks or real-time monitoring triggers—a textbook cyber hygiene failure.

MGM refused to pay the ransom, but the damage was done: $100M in lost revenue, lawsuits, and 30M+ records exposed.

1. MFA, Strong Passwords & Password Managers (NIST SP 800-53: IA-2, AC-7)

Businesses: Enforce company-wide MFA and train your help desk to verify every request. If MGM had followed NIST IA-2, this breach wouldn't have happened.

- Individuals: Ditch weak passwords. Use passphrases like 'Ph1llyC15A!' and enable MFA on everything—email, banking, work accounts.


> 📌 Use a Password Manager: Weak passwords and password reuse are significant security risks. A password manager, like Bitwarden or 1Password, can generate and store unique, complex passwords** for every account. NIST recommends using password managers to eliminate the need for users to remember multiple passwords, reducing password fatigue and improving security.

> 📌 Reality Check: I've seen one-time codes stop ransomware cold. Use them.
2. Patch & Update Everything (NIST SP 800-53: SI-2)

- Businesses: MGM's 10-day outage hints at poor patching. Schedule monthly updates, automate scanning with Nessus, and patch before attackers exploit the gaps.

- Individuals: Hit Update! Those iOS prompts aren't nagging—they're saving you from zero-days.


> 📌 Reality Check: Unpatched endpoints lead straight to breaches.
3. Secure Configurations & Endpoint Protection (NIST SP 800-53: CM-6, SC-7)

- Businesses: MGM's admin access fell in 10 minutes—likely default settings, open ports, or lax role-based access controls. Scan configurations quarterly, lock down admin privileges, and use least privilege access.

- Individuals: Secure your Wi-Fi—use WPA3, change default passwords, and disable unused services.


> 📌 Reality Check: I've run Nessus scans that found open ports and misconfigs that could have ended in breaches.
Cyber Hygiene: It's Not Optional

MGM is proof that basic cyber hygiene failures cost millions. Whether you're a business or an individual, take NIST recommendations seriously:

Businesses:

- ✅ Train your help desk—social engineering is real.
- ✅ Roll out MFA company-wide—one weak account is all it takes.
- ✅ Patch before attackers exploit it—monthly, no excuses.
- ✅ Scan & lock down configs—misconfigurations are hacker gold.
Individuals:

- ✅ Stop using 'password123.' Use passphrases & MFA everywhere.
- ✅ Use a password manager—secure, unique passwords for all accounts.
- ✅ Update weekly—those patches close the holes attackers exploit.
- ✅ Lock your router—no open networks, no weak passwords.
- ✅ Scrub your LinkedIn—oversharing helps hackers.
What's Next?

I'm building cyber hygiene scripts on GitHub (samson-2369)—password strength checkers, config scanners, and tools to keep Region 3 secure. Stay tuned—I'll unpack more NIST insights and real-world security lessons in future posts.

