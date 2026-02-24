# 🔍 Wireshark Packet Analysis & ARP Behavior Study

> Foundational study of ARP protocol behavior, packet capture techniques, and introduction to ARP spoofing detection concepts.

---

## 🎯 Objective

To understand how ARP works in a local network and observe network traffic using Wireshark.

Future goal:
- Identify abnormal ARP behavior
- Understand how ARP spoofing (MITM) attacks operate
- Recognize indicators of suspicious network activity

---

## 🧠 Concepts Covered

- What is ARP?
- How ARP resolves MAC addresses
- Broadcast vs Unicast ARP traffic
- How ARP spoofing works
- Basics of Man-in-the-Middle (MITM) attacks

---

## 🛠️ Tools Used

- Kali Linux
- Wireshark
- (Future) Bettercap for ARP spoofing simulation

---

## 🖥️ Lab Environment

- VirtualBox
- Kali Linux VM
- Ubuntu VM (Target)
- Bridged / Internal Networking

---

## 📡 Packet Capture Process

1. Open Wireshark
2. Select active network interface
3. Start packet capture
4. Apply ARP filter:

```bash
arp
```

5. Observe ARP request and reply packets

---

## 🔎 Observations (To Be Updated After Demo)

- [ ] Observed ARP request broadcast
- [ ] Observed ARP reply
- [ ] Identified source and destination MAC addresses
- [ ] Analyzed packet structure
- [ ] Compared normal ARP behavior vs suspicious activity

---

## 🚨 ARP Spoofing Study (Conceptual Stage)

Understanding:

- How an attacker sends fake ARP replies
- How a victim updates ARP cache incorrectly
- How traffic can be redirected to attacker
- How Wireshark can detect duplicate ARP replies

(Future: Practical demonstration with Bettercap)

---

## 🛡️ Detection Indicators (To Expand After Practical Demo)

- Multiple ARP replies for same IP
- Inconsistent MAC address mapping
- Unusual broadcast frequency
- Unexpected gateway MAC changes

---

## 📚 Learning Outcome

This study builds foundational skills required for:

- SOC traffic monitoring
- Network anomaly detection
- MITM attack identification
- Packet-level investigation
