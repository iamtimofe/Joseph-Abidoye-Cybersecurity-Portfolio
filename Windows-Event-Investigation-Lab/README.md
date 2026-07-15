# 🛡️ Windows Security Event Investigation Lab

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-blue)
![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94)
![SOC](https://img.shields.io/badge/SOC-Blue%20Team-success)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red)
![License](https://img.shields.io/badge/License-MIT-green)

---

# Table of Contents

- [Project Overview](#project-overview)
- [Lab Environment](#lab-environment)
- [Tools Used](#tools-used)
- [Investigation Workflow](#investigation-workflow)
- [Investigation Phases](#investigation-phases)
  - [Phase 1: Network Enumeration](#phase-1-network-enumeration)
  - [Phase 2: Failed Logon Investigation](#phase-2-failed-logon-investigation)
  - [Phase 3: Successful Logon Investigation](#phase-3-successful-logon-investigation)
  - [Phase 4: User Account Creation Investigation](#phase-4-user-account-creation-investigation)
  - [Phase 5: Privilege Escalation Investigation](#phase-5-privilege-escalation-investigation)
  - [Phase 6: Remote SMB Authentication Investigation](#phase-6-remote-smb-authentication-investigation)
- [Investigation Timeline](#investigation-timeline)
- [Event Summary](#event-summary)
- [MITRE ATT&CK Mapping](#mitre-attck-mapping)
- [Indicators of Compromise (IOCs)](#indicators-of-compromise-iocs)
- [Evidence and Screenshots](#evidence-and-screenshots)
- [Challenges Encountered and Resolutions](#challenges-encountered-and-resolutions)
- [Final Incident Report](#final-incident-report)
- [Repository Structure](#repository-structure)
- [Skills Demonstrated](#skills-demonstrated)
- [Key Findings](#key-findings)
- [Learning Outcomes](#learning-outcomes)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

# Project Overview

This project demonstrates a hands-on **Security Operations Center (SOC) investigation** performed inside an isolated VirtualBox laboratory environment using **Windows Server 2022** and **Kali Linux**.

The goal of this project was to simulate realistic security events, investigate Windows Security Logs, analyze authentication activity, identify suspicious behavior, collect Indicators of Compromise (IOCs), correlate evidence, and document findings using a structured SOC investigation methodology.

The lab simulates common enterprise security scenarios including:

- Network reconnaissance
- SMB enumeration
- Authentication testing
- Failed login attempts
- Successful authentication events
- User account creation
- Privilege escalation
- Remote SMB authentication failures
- IOC collection
- Incident documentation

---

# Lab Environment

| Component | Description |
|-----------|-------------|
| Hypervisor | Oracle VirtualBox |
| Target Machine | Windows Server 2022 |
| Attacker Machine | Kali Linux |
| Network Type | Internal Virtual Network |
| Target IP Address | 192.168.100.10 |
| Attacker IP Address | 192.168.100.20 |

---

# Tools Used

## Windows Tools

- Windows Event Viewer
- PowerShell
- Command Prompt

## Kali Linux Tools

- Nmap
- NetExec (CrackMapExec)
- SMB Tools

## Documentation Tools

- Git
- GitHub

---

# Investigation Workflow

The investigation followed a typical SOC analyst workflow:

```
              Lab Setup
                  │
                  ▼
        Network Enumeration
                  │
                  ▼
       Authentication Testing
                  │
                  ▼
       Windows Security Logs
                  │
                  ▼
          Event Analysis
                  │
                  ▼
          IOC Collection
                  │
                  ▼
        Incident Reporting
```

---

# Investigation Phases

# Phase 1: Network Enumeration

## Objective

Identify exposed services and available ports on the Windows Server before conducting authentication testing.

## Tools Used

- Nmap
- NetExec

## Commands Used

```bash
nmap -Pn -p 445 192.168.100.10

nmap -Pn -p 5985 192.168.100.10

netexec smb 192.168.100.10
```

## Findings

The enumeration identified:

- SMB service running on port 445
- WinRM service running on port 5985
- Windows Server 2022 detected
- SMBv1 disabled
- SMB signing disabled

## Report

[Network Enumeration Report](Event_Analysis/network_enumeration.md)

## Screenshot Evidence

![Network Enumeration](Screenshots/00_network_enumeration.png)

---

# Phase 2: Failed Logon Investigation

## Event ID

**4625 — Failed Logon**

## Objective

Investigate unsuccessful authentication attempts recorded within Windows Security Logs.

## Investigation Details

The analysis focused on:

- Target account
- Logon type
- Authentication method
- Failure reason
- Source information

## Report

[Event 4625 Failed Logon Investigation](Event_Analysis/event_4625_bruteforce.md)

## Screenshot Evidence

![Failed Login](Screenshots/01_failed_login.png)

---

# Phase 3: Successful Logon Investigation

## Event ID

**4624 — Successful Logon**

## Objective

Analyze successful authentication activity and determine the legitimacy of login events.

## Investigation Details

Reviewed:

- User account
- Logon type
- Authentication details
- Timestamp information

## Report

[Event 4624 Successful Logon Investigation](Event_Analysis/event_4624_successful_logon.md)

## Screenshot Evidence

![Successful Logon](Screenshots/02_successful_logon.png)

---

# Phase 4: User Account Creation Investigation

## Event ID

**4720 — User Account Created**

## Objective

Detect and investigate the creation of new Windows user accounts.

## Investigation Details

Reviewed:

- Created account
- Account creation timestamp
- Account creator

## Report

[User Account Creation Investigation](Event_Analysis/event_4720_user_creation.md)

## Screenshot Evidence

![User Created](Screenshots/03_user_created.png)

---

# Phase 5: Privilege Escalation Investigation

## Event ID

**4732 — User Added to Local Administrators Group**

## Objective

Identify unauthorized privilege assignments and administrative group changes.

## Investigation Details

Detected:

- User added to administrator group
- Privilege escalation activity
- Administrative permission modification

## Report

[Privilege Escalation Investigation](Event_Analysis/event_4732_group_membership.md)

## Screenshot Evidence

![Privilege Escalation](Screenshots/04_group_added.png)

---

# Phase 6: Remote SMB Authentication Investigation

## Objective

Perform remote authentication testing from Kali Linux and analyze resulting Windows Security Events.

A failed SMB authentication attempt was performed using NetExec.

Windows generated **Event ID 4625**.

## Event Details

| Field | Value |
|------|-------|
| Event ID | 4625 |
| Logon Type | 3 (Network) |
| Source IP | 192.168.100.20 |
| Target Host | 192.168.100.10 |
| Target Account | Administrator |
| Authentication | NTLM |

## Report

[SMB Authentication Investigation](Event_Analysis/event_4625_bruteforce.md)

## Screenshot Evidence

![Failed SMB Authentication](Screenshots/05_failed_smb_logon.png)

---

# Investigation Timeline

A chronological timeline of all investigated security events:

[Investigation Timeline](Event_Analysis/timeline.md)

---

# Event Summary

Summary of all analyzed Windows Security Events:

[Event Summary](Event_Analysis/event_summary.md)

---

# MITRE ATT&CK Mapping

| Technique | Technique ID |
|-----------|--------------|
| Valid Accounts | T1078 |
| Account Manipulation | T1098 |
| Brute Force | T1110 |
| Password Guessing | T1110.001 |
| Create Account | T1136 |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Source IP | 192.168.100.20 |
| Target Host | 192.168.100.10 |
| Target Account | Administrator |
| Event IDs | 4624, 4625, 4720, 4732 |
| Authentication | NTLM |

## IOC Report

[IOC Report](IOC_Report/iocs.txt)

---

# Evidence and Screenshots

All investigation evidence collected during the lab:

## Evidence Files

- [Investigation Notes](Evidence/investigation_notes.txt)
- [Network Scan Results](Evidence/network_scan.txt)

## Screenshot Evidence

| Screenshot | Description |
|------------|-------------|
| 00_network_enumeration.png | Network enumeration results |
| 01_failed_login.png | Failed authentication event |
| 02_successful_logon.png | Successful authentication event |
| 03_user_created.png | User account creation event |
| 04_group_added.png | Privilege escalation event |
| 05_failed_smb_logon.png | Remote SMB authentication failure |

---

# Challenges Encountered and Resolutions

## 1. Virtual Machine Network Connectivity

### Challenge

Initially, Kali Linux and Windows Server could not communicate.

Symptoms:

- Destination Host Unreachable
- Failed ping requests
- Incorrect network communication

### Resolution

The issue was resolved by:

- Configuring both virtual machines on the same VirtualBox Internal Network.
- Assigning static IP addresses.

| Machine | IP Address |
|---------|------------|
| Windows Server 2022 | 192.168.100.10 |
| Kali Linux | 192.168.100.20 |

Connectivity was verified using ICMP tests.

---

## 2. Windows Firewall Blocking ICMP

### Challenge

Ping requests failed even after configuring correct IP addresses.

### Cause

Windows Firewall was blocking ICMP traffic.

### Resolution

Firewall settings were temporarily adjusted inside the isolated lab environment to allow connectivity testing.

---

## 3. Generating Remote Authentication Events

### Challenge

Initial failed login attempts only produced local authentication records.

### Resolution

Remote SMB authentication attempts were performed using NetExec from Kali Linux.

This generated:

- Event ID 4625
- Logon Type 3
- Remote source IP visibility

---

## 4. Windows Event Log Analysis

### Challenge

Large volumes of Windows logs made identifying relevant events difficult.

### Resolution

Focused investigation on important security event IDs:

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4720 | User Account Created |
| 4732 | Added to Administrators Group |

---

## 5. GitHub Repository Organization

### Challenge

Maintaining a professional structure for reports, evidence, screenshots, and documentation.

### Resolution

Created organized folders for:

- Event analysis
- Evidence
- IOC reports
- Screenshots
- Documentation

---

# Final Incident Report

Complete SOC investigation report:

[Final Incident Report](IOC_Report/Final_Incident_Report.md)

---

# Repository Structure

```text
Windows-Event-Investigation-Lab

├── Event_Analysis
│   ├── event_4624_successful_logon.md
│   ├── event_4625_bruteforce.md
│   ├── event_4720_user_creation.md
│   ├── event_4732_group_membership.md
│   ├── event_summary.md
│   ├── network_enumeration.md
│   └── timeline.md
│
├── Evidence
│   ├── investigation_notes.txt
│   └── network_scan.txt
│
├── IOC_Report
│   ├── Final_Incident_Report.md
│   └── iocs.txt
│
├── Screenshots
│   ├── 00_network_enumeration.png
│   ├── 01_failed_login.png
│   ├── 02_successful_logon.png
│   ├── 03_user_created.png
│   ├── 04_group_added.png
│   └── 05_failed_smb_logon.png
│
├── README.md
└── LICENSE
```

---

# Skills Demonstrated

- SOC Investigation
- Windows Security Event Analysis
- Authentication Monitoring
- Network Enumeration
- SMB Investigation
- Privilege Escalation Detection
- IOC Collection
- Incident Response
- Event Correlation
- MITRE ATT&CK Mapping
- Technical Documentation
- Git & GitHub

---

# Key Findings

- Investigated Windows Security Events generated from simulated attack scenarios.
- Identified failed and successful authentication attempts.
- Detected user account creation activity.
- Verified privilege escalation events.
- Performed SMB enumeration from Kali Linux.
- Correlated network activity with Windows Event Logs.
- Produced a complete SOC-style incident investigation report.

---

# Learning Outcomes

This project strengthened practical skills in:

- Windows Event Log analysis
- SOC alert investigation
- Authentication monitoring
- Endpoint investigation
- Network-based attack analysis
- Threat detection methodology
- Incident documentation

---

# Future Improvements

Planned improvements:

- Deploy Sysmon for enhanced endpoint telemetry.
- Integrate logs with Wazuh SIEM.
- Create Sigma detection rules.
- Build Splunk dashboards.
- Simulate Active Directory attacks.
- Add lateral movement detection scenarios.

---

# Author

## Joseph Abidoye

SOC Analyst | Blue Team | Threat Detection | Incident Response | Windows Security | Network Security

GitHub:

https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio

---

# License

This project is licensed under the MIT License.
