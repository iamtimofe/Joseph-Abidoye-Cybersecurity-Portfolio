# Sysmon Event ID 3 – Network Connection

## Overview

Sysmon Event ID 3 records outbound network connections initiated by processes on the endpoint. Unlike standard Windows logs, Sysmon provides detailed information about the process responsible for the connection, destination IP address, destination port, protocol, and user context.

This event is essential for identifying command-and-control (C2) communication, malware beaconing, unauthorized remote connections, and data exfiltration.

---

## Lab Objective

The objective of this exercise was to generate outbound network traffic and analyze the network connection events captured by Microsoft Sysmon.

---

## Lab Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows Server 2022 |
| Monitoring Tool | Microsoft Sysmon |
| Log Source | Microsoft-Windows-Sysmon/Operational |
| Hypervisor | Oracle VirtualBox |

---

## Test Activity

The following activities generated outbound network connections:

- Browsing websites using Google Chrome
- Running DNS lookups with `nslookup`
- Downloading the Sysmon configuration file
- Accessing external Internet resources

Sysmon successfully recorded the associated network connections.

---

## Event Summary

| Field | Value |
|-------|-------|
| Event ID | 3 |
| Event Name | Network Connection |
| Log Name | Microsoft-Windows-Sysmon/Operational |
| Severity | Information |

---

## Key Fields Observed

The following information was available in the event:

- Process GUID
- Process ID
- Image
- User
- Protocol
- Initiated
- Source IP Address
- Source Port
- Destination IP Address
- Destination Port
- Destination Hostname

---

## Investigation

Each outbound network connection was linked to the originating process, allowing the activity to be traced back to the application responsible.

This level of visibility enables investigators to determine:

- Which application initiated the connection
- Where the connection was made
- Which port and protocol were used
- Whether the communication was expected or suspicious

---

## Security Relevance

Network Connection events are commonly used to detect:

- Malware beaconing
- Command-and-Control (C2) traffic
- Reverse shells
- Unauthorized remote access
- Data exfiltration
- Suspicious outbound connections

---

## MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1071 | Application Layer Protocol |
| T1105 | Ingress Tool Transfer |
| T1041 | Exfiltration Over C2 Channel |

---

## Detection Opportunities

SOC analysts should investigate:

- PowerShell establishing Internet connections
- Command Prompt connecting externally
- Browsers spawning unexpected outbound traffic
- Connections to uncommon ports
- Known malicious IP addresses
- Repeated outbound connections to unknown destinations

---

## Correlation Opportunities

Network Connection events should be correlated with:

- Event ID 1 – Process Creation
- Event ID 22 – DNS Query
- Windows Firewall logs
- Proxy logs
- SIEM alerts

This provides a complete picture of endpoint network activity.

---

## Lessons Learned

This exercise demonstrated how Sysmon significantly improves visibility into endpoint communications.

By identifying both the process and destination involved in every outbound connection, analysts can quickly detect suspicious communications and investigate potential compromises.

---

## Conclusion

Event ID 3 provides detailed telemetry about outbound network communications and is a critical data source for threat hunting, malware analysis, and incident response.

Monitoring these events enables SOC analysts to identify suspicious network behavior before it develops into a larger security incident.
