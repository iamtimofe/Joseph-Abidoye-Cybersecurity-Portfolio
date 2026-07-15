# 🛡️ Windows Security Event Investigation Lab

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-blue)
![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94)
![SOC](https://img.shields.io/badge/SOC-Investigation-success)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red)
![License](https://img.shields.io/badge/License-MIT-green)

## Project Overview

This project demonstrates a hands-on **Windows Security Event Investigation** performed in a controlled lab environment using **Windows Server 2022** and **Kali Linux** running in Oracle VirtualBox.

The investigation follows a typical Security Operations Center (SOC) workflow, beginning with network reconnaissance, followed by authentication testing, Windows Event Log analysis, incident documentation, IOC collection, and the production of a final incident report.

The lab simulates realistic administrative and security events that SOC analysts investigate daily, including:

- Failed authentication attempts
- Successful user logons
- User account creation
- Privilege escalation
- Remote SMB authentication failures
- Network enumeration

---

# Objectives

- Investigate Windows Security Events.
- Analyze authentication activity.
- Detect account creation and privilege changes.
- Perform network reconnaissance.
- Simulate remote authentication attempts.
- Collect Indicators of Compromise (IOCs).
- Correlate multiple Windows Security Events.
- Produce a professional SOC investigation report.

---

# Lab Environment

| Component | Description |
|-----------|-------------|
| Hypervisor | Oracle VirtualBox |
| Target Machine | Windows Server 2022 |
| Attacker Machine | Kali Linux |
| Network | Internal Virtual Network |
| Target IP | 192.168.100.10 |
| Attacker IP | 192.168.100.20 |

---

# Tools Used

- Windows Event Viewer
- NetExec (CrackMapExec)
- Nmap
- Command Prompt
- PowerShell
- Kali Linux
- Windows Server 2022
- Git
- GitHub

---

# Investigation Workflow

```text
Network Setup
      │
      ▼
Network Enumeration
      │
      ▼
Authentication Testing
      │
      ▼
Windows Security Events
      │
      ▼
IOC Collection
      │
      ▼
Event Correlation
      │
      ▼
Incident Reporting
```

---

# Investigation Phases

## Phase 1 — Failed Local Logon Investigation

### Event ID

4625 – Failed Logon

### Objective

Investigate a failed local authentication attempt.

### Report

- [Event 4625 Analysis](Event_Analysis/event_4625_bruteforce.md)

### Screenshot

![Failed Login](Screenshots/01_failed_login.png)

---

## Phase 2 — Successful Logon Investigation

### Event ID

4624 – Successful Logon

### Objective

Analyze a successful Windows authentication event.

### Report

- [Successful Logon Investigation](Event_Analysis/event_4624_successful_logon.md)

### Screenshot

![Successful Logon](Screenshots/02_successful_logon.png)

---

## Phase 3 — User Account Creation

### Event ID

4720 – User Account Created

### Objective

Investigate the creation of a new Windows user account.

### Report

- [User Account Creation Investigation](Event_Analysis/event_4720_user_creation.md)

### Screenshot

![User Account Created](Screenshots/03_user_created.png)

---

## Phase 4 — Privilege Escalation Investigation

### Event ID

4732 – User Added to Administrators Group

### Objective

Investigate administrative privilege assignment.

### Report

- [Group Membership Investigation](Event_Analysis/event_4732_group_membership.md)

### Screenshot

![Group Membership](Screenshots/04_group_added.png)

---

## Phase 5 — Network Enumeration

The Windows Server was enumerated from Kali Linux before authentication testing.

### Commands Used

```bash
nmap -Pn -p 445 192.168.100.10

nmap -Pn -p 5985 192.168.100.10

netexec smb 192.168.100.10
```

### Findings

- SMB (445/TCP) Open
- WinRM (5985/TCP) Open
- Windows Server 2022 identified
- SMBv1 Disabled
- SMB Signing Disabled

### Report

- [Network Enumeration](Event_Analysis/network_enumeration.md)

### Screenshot

![Network Enumeration](Screenshots/00_network_enumeration.png)

---

## Phase 6 — Remote SMB Authentication Investigation

A failed SMB authentication attempt was generated from Kali Linux using NetExec.

Windows recorded the activity as **Event ID 4625**.

### Event Details

| Field | Value |
|--------|-------|
| Event ID | 4625 |
| Logon Type | 3 (Network) |
| Source IP | 192.168.100.20 |
| Target Account | Administrator |
| Authentication | NTLM |

### Report

- [SMB Authentication Investigation](Event_Analysis/event_4625_bruteforce.md)

### Screenshot

![Failed SMB Authentication](Screenshots/05_failed_smb_logon.png)

---

# Investigation Timeline

A chronological timeline of all investigated events is available below.

- [Investigation Timeline](Event_Analysis/timeline.md)

---

# Event Summary

A summary of all investigated Windows Security Events.

- [Event Summary](Event_Analysis/event_summary.md)

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Source IP | 192.168.100.20 |
| Target Host | 192.168.100.10 |
| Target Account | Administrator |
| Event IDs | 4624, 4625, 4720, 4732 |
| Authentication | NTLM |

Detailed IOC list:

- [IOC Report](IOC_Report/iocs.txt)

---

# Final Incident Report

The complete SOC investigation report is available below.

- [Final Incident Report](IOC_Report/Final_Incident_Report.md)

---

# Evidence

Supporting evidence collected during the investigation.

- [Investigation Notes](Evidence/investigation_notes.txt)
- [Network Scan Results](Evidence/network_scan.txt)

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

# Skills Demonstrated

- Windows Event Log Analysis
- Authentication Investigation
- Network Enumeration
- SMB Authentication Analysis
- Privilege Escalation Detection
- IOC Collection
- Incident Documentation
- Event Correlation
- Threat Investigation
- MITRE ATT&CK Mapping
- Technical Reporting
- Git & GitHub Documentation

---

# Challenges Encountered

## 1. Virtual Machine Network Connectivity

### Challenge

Initially, Kali Linux and Windows Server could not communicate.

Symptoms included:

- Destination Host Unreachable
- Network is unreachable
- APIPA (169.254.x.x) addressing
- Failed ping requests

### Resolution

- Configured both virtual machines on the same VirtualBox Internal Network.
- Assigned static IPv4 addresses:
  - Windows Server: `192.168.100.10`
  - Kali Linux: `192.168.100.20`
- Verified routing.
- Confirmed connectivity with successful ICMP tests.

---

## 2. Windows Firewall Blocking ICMP

### Challenge

Even after assigning IP addresses, ping requests initially failed.

### Resolution

Temporarily disabled Windows Firewall for the isolated lab environment to validate connectivity and continue testing.

---

## 3. Remote Authentication Testing

### Challenge

Initial failed logon events only generated local authentication records.

### Resolution

Used **NetExec** from Kali Linux to perform remote SMB authentication attempts, successfully generating **Event ID 4625** with the remote source IP (`192.168.100.20`) for investigation.

---

## 4. GitHub Documentation

### Challenge

Ensuring the repository was organized and easy to navigate.

### Resolution

Created a structured project layout with:

- Event reports
- IOC reports
- Evidence
- Investigation timeline
- Screenshots
- Final incident report
- Comprehensive README

---

# Repository Structure

```text
Windows-Event-Investigation-Lab
│
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

# Key Takeaways

This lab demonstrates practical SOC skills including Windows log analysis, authentication investigations, network reconnaissance, event correlation, IOC collection, and technical documentation. It reflects a structured approach to investigating Windows security events in a controlled environment and highlights the importance of combining host-based evidence with network activity to understand potential security incidents.

---

# Future Improvements

- Deploy Sysmon for enhanced endpoint telemetry.
- Integrate Windows logs with Wazuh SIEM.
- Develop Sigma detection rules.
- Build Splunk dashboards for authentication monitoring.
- Expand the lab with Active Directory and lateral movement detection scenarios.

---

# Author

**Joseph Abidoye**

SOC Analyst | Blue Team | Threat Detection | Incident Response | Windows Security | Network Security

- **GitHub:** https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio
- **LinkedIn:** *(Add your LinkedIn profile URL)*

---

# License

This project is licensed under the MIT License.
