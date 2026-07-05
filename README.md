# 🔐 Joseph Abidoye – Cybersecurity Portfolio
> Aspiring SOC Analyst | Blue Team Focus | Network Security, Cloud Security & Lab-Based Learning

---

## 👨🏽‍💻 About Me

I began my cybersecurity journey in November 2025 at AltSchool Africa, focusing on building strong foundations in networking, Linux systems, cloud security, and security operations.

My learning approach is hands-on and lab-driven, with emphasis on understanding how networks function, how access is controlled, how threats are detected, and how security policies are enforced — across on-prem, cloud, and OSINT/reconnaissance contexts.

My long-term goal is to become a Security Operations Center (SOC) Analyst specializing in threat detection, monitoring, and incident response.

---

## 🚀 Featured Projects

### ☁️ AWS Honeytoken Detection & Automated Kill-Switch (Cloud Security)

This project simulates a cloud breach detection and automated response pipeline using a honeytoken secret in AWS Secrets Manager as bait.

Key Components Implemented:
- Dual detection paths: CloudWatch Metric Filters/Alarms **and** EventBridge rules
- Real-time SNS email alerting on unauthorized secret access
- Automated Lambda kill-switch that strips IAM permissions from a compromised user
- Forensic evidence chain: CloudTrail logs, alert emails, IAM state before/after
- Comparative security analysis of detection speed (EventBridge vs. CloudWatch) for a banking-grade use case

📂 View Project:
➡️ [AWS Honeytoken & Kill-Switch Project](Cloud-Security/AWS-Honeytoken-Kill-Switch/README.md)

---

### 🕵️ External Reconnaissance & Attack Surface Mapping (OSINT)

A full reconnaissance and footprinting engagement against an authorized lab domain, combining passive OSINT with active scanning to build a prioritized attack surface.

Key Components Implemented:
- Passive OSINT: Amass, Recon-ng, WHOIS, dig, theHarvester, Google Dorking
- Active scanning: Nmap host discovery, full port/version scan, aggressive scan
- Attack Surface Data Flow Diagram (DFD) mapping entry points to backend microservices
- Risk-based target prioritization (API gateway, legacy web server, SSH, mail server, payment subdomain)

📂 View Project:
➡️ [External Recon & Attack Surface Mapping](OSINT-Recon/AltSchoolAfrica-Recon-Footprinting/README.md)

---

### 📡 Secure Branch Office Network Design (VLAN + ACL Implementation)

This project demonstrates practical implementation of enterprise-style network segmentation and access control using Cisco Packet Tracer.

Key Components Implemented:
- VLAN segmentation (Admin, Sales, IT)
- Inter-VLAN routing (Router-on-a-Stick)
- Trunk port configuration
- Access Control List (ACL) enforcement
- Security validation using ping testing
- Visual topology documentation

📂 View Project:
➡️ [Network Segmentation & ACL Project](Networking/Network-Segmentation-and-ACL.md)

---

### 🛡️ Wazuh Security Monitoring and Compliance (SIEM Lab)

This project showcases the use of **Wazuh SIEM** for real-time security monitoring and compliance auditing.
It highlights how alerts are generated, analyzed, and tied to organizational compliance requirements.

Key Components Implemented:
- Accessed Wazuh dashboard and verified agent connectivity
- Explored logs under *Security Events* and *System Auditing*
- Identified a **File Integrity Monitoring alert**:
  *Integrity checksum changed for `c:\assessment2\joseph_abidoye.txt`*
- Analyzed the alert:
  - **Technical Explanation:** Wazuh detected a mismatch in cryptographic hash values (SHA1/SHA256), indicating file modification.
  - **Importance:** File integrity monitoring is critical for compliance frameworks (e.g., PCI DSS, ISO 27001). Detecting unauthorized changes helps prevent insider threats, malware persistence, and data tampering.

📂 View Project:
➡️ [Wazuh Security Monitoring Project](Wazuh-Security_Monitoring/README.md)

---

## 🧪 Hands-On Labs

### 🔑 Applied Cryptography & Secure Web Server Lab

Hands-on lab covering symmetric and asymmetric encryption, plus a live demonstration of why HTTP exposes data in transit while HTTPS protects it.

Key Components Implemented:
- AES-256-CBC symmetric encryption/decryption with OpenSSL
- RSA-2048 asymmetric key generation, encryption, and decryption
- Apache HTTP server setup with Wireshark packet capture showing plaintext traffic
- Apache HTTPS setup with a self-signed certificate, showing TLS handshake and encrypted traffic in Wireshark

📂 View Lab:
➡️ [Applied Cryptography & HTTPS Lab](Cryptography/Applied-Cryptography-HTTPS-Lab/README.md)

---

### 🖥️ Home Virtual Lab Setup (Kali Linux + Ubuntu)
- Built a virtual lab using VirtualBox
- Configured bridged networking
- Verified IP assignments using `ip a`
- Practiced Linux networking fundamentals
- Troubleshot configuration issues

📂 View Lab:
➡️ [Home Virtual Lab Documentation](Labs/Home-Virtual-Lab-Setup.md)

---

## 🛠️ Technical Foundations

### Networking
- VLAN Configuration
- Inter-VLAN Routing
- Access Control Lists (ACLs)
- Network Segmentation Design
- IP Addressing & Subnetting

### Cloud Security
- AWS CloudTrail, CloudWatch, EventBridge
- AWS Lambda & IAM automated remediation
- AWS Secrets Manager
- Honeytoken-based threat detection

### OSINT & Reconnaissance
- Amass, Recon-ng, theHarvester
- WHOIS & DNS enumeration (dig)
- Nmap host discovery & service/version scanning
- Attack surface mapping (DFD) and risk prioritization

### Cryptography
- Symmetric encryption (AES-256-CBC)
- Asymmetric encryption (RSA-2048)
- TLS/SSL certificate generation
- HTTP vs. HTTPS traffic analysis (Wireshark)

### Systems
- Linux (Kali & Ubuntu)
- Basic Command-Line Operations
- Virtual Lab Deployment

### Security Principles
- Least Privilege
- Department-Based Access Control
- Logical Network Isolation
- Defense-in-Depth
- Continuous Monitoring & Automated Response

---

## 📈 Current Learning Focus
- Deepening SIEM detection engineering (Wazuh use cases)
- Packet analysis fundamentals using Wireshark
- Understanding ARP protocol behavior and ARP spoofing concepts
- Building a broader security monitoring and incident response mindset

---

## 🎯 Career Objective

Seeking opportunities in:
- SOC Analyst (Entry-Level / Junior)
- NOC (Network Operations Center)
- Cloud Security Analyst (Entry-Level)
- IT Support / Entry-Level Network Security

Open to remote and on-site opportunities.

---

## 🌍 Location
Nigeria

---

> “Security is built on strong fundamentals, disciplined practice, and continuous improvement.”
