---
layout: post
title: "Building a Cyber Defense Development Environment in a Virtual Machine"
date: 2025-04-10
categories: blog
tags: [homelab Python tools development]
excerpt: "In today's rapidly evolving cyber threat landscape, having a robust and flexible cybersecurity development environment is crucial for professionals aiming to enhance their defensive capabilities. This"
---

In today's rapidly evolving cyber threat landscape, having a robust and flexible cybersecurity development environment is crucial for professionals aiming to enhance their defensive capabilities. This blog post provides a comprehensive guide to setting up a powerful, portable development environment within an Ubuntu XFCE virtual machine. Designed specifically to support AI-driven cybersecurity experiments and sophisticated network defense tools, this environment is perfect for both beginners eager to learn and experienced professionals seeking to expand their skillset. Follow along step-by-step to create your own secure and versatile cyber defense lab.

Step 1: Set Up the Base Environment

Download and install VirtualBox. Then, get an Ubuntu XFCE ISO image for a lightweight Linux desktop experience. Create a new virtual machine with recommended settings: 2 GB RAM, 20 GB disk space. Mount the ISO and follow the installation steps. After installation, configure network settings to either NAT (internet access) or Bridged Adapter (direct access to your home network).


> 💻 Terminal:
    sudo apt update
    sudo apt install python3 python3-pip python3-venv
Step 2: Create an Isolated Python Environment

Isolate your development environment using Python's built-in venv module. This ensures any installed libraries won't interfere with system-wide packages.


> 💻 Terminal:
    python3 -m venv ai-envsource ai-env/bin/activatepip install tensorflow torch gymnasium stable-baselines3 jupyter
Step 3: Build Your First Cyber Defense Agent

Start simple with a ping-based host discovery agent.


> 💻 Terminal:
    pip install ping3
# Python Script:from ping3import ping

    hosts = ["192.168.1." + str(i) for i in range(1, 255)]active_hosts = []
    for host in hosts:
    response = ping(host, timeout=1)
    if response:
print(f"Host {host} is active.")

    active_hosts.append(host)print(f"Active hosts: {active_hosts}")
Step 4: Upgrade to ARP Scanning with Scapy

Move beyond ICMP to ARP scanning for more reliable local network discovery.


> 💻 Terminal:
    python3 -m venv scanner-env
    source scanner-env/bin/activate
    pip install scapy netifaces
# Python Script:

    from scapy.all import ARP, Ether, srp
    import netifaces
    def arp_scan(network):
    arp = ARP(pdst=network)
    ether = Ether(dst="ff:ff:ff:ff:ff:ff")
    packet = ether/arp
    result = srp(packet, timeout=3, verbose=0)[0]
    devices = []
    for sent, received in result:
    devices.append({'ip': received.psrc, 'mac': received.hwsrc})
return devices

Step 5: Resolve Permissions and Virtual Environment Access

Run your ARP scanning script with root privileges while preserving the virtual environment.


> 💻 Terminal:
    sudo ./scanner-env/bin/python arp_host_scanner.py
Step 6: Enhance with Hostname Resolution

Improve scan output clarity using reverse DNS lookups.

# Python Snippet:

    import socket
    def resolve_hostname(ip):
try:

return socket.gethostbyaddr(ip)[0]

except socket.herror:

return 'Unknown'

Step 7: Validate and Log

Scan your network and log the results to timestamped files for review.

# Python Snippet:

    import datetime
    log_filename = datetime.datetime.now().strftime("logs/scan_%Y%m%d_%H%M%S.txt")
    with open(log_filename, 'w') as log_file:
    for device in devices:
hostname = resolve_hostname(device['ip'])

    log_file.write(f"IP: {device['ip']} MAC: {device['mac']} Hostname: {hostname}\n")
?? What’s Next

- Compare logs to identify new or unauthorized devices- Analyze network trends using Jupyter notebooks- Integrate AI for anomaly detection and alertingThis development environment blends AI, automation, and practical cyber defense—all inside a convenient, portable VM. Stay tuned for future posts where I'll build this foundation into a fully operational mini blue-team SOC lab.
