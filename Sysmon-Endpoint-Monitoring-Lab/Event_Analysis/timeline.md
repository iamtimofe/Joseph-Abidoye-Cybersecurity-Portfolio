# Investigation Timeline

## Overview

This timeline summarizes the sequence of activities performed during the Sysmon Endpoint Monitoring Lab. Each action generated telemetry that was captured and analyzed using Microsoft Sysmon.

---

| Time | Activity | Sysmon Event |
|------|----------|--------------|
| 1 | Microsoft Sysmon installed on Windows Server 2022 | Installation |
| 2 | Sysmon configuration imported | Configuration |
| 3 | Command Prompt and PowerShell executed | Event ID 1 |
| 4 | Google Chrome launched | Event ID 1 |
| 5 | Internet browsing performed | Event ID 3 |
| 6 | DNS lookups generated | Event ID 22 |
| 7 | Sysmon configuration file downloaded | Event ID 11 |
| 8 | Event Viewer opened for investigation | Analysis |
| 9 | Relevant Sysmon events documented | Documentation |
| 10 | IOC report created | Reporting |

---

## Investigation Flow

Install Sysmon
│
▼
Import Configuration
│
▼
Generate Endpoint Activity
│
├──────────────┐
▼ ▼
Processes Network Traffic
(Event 1) (Event 3)
│ │
└──────┬───────┘
▼
DNS Queries
(Event 22)
│
▼
File Download
(Event 11)
│
▼
Event Investigation
│
▼
IOC Collection
│
▼
Final Incident Report

---

## Summary

The generated Sysmon events were analyzed in chronological order to reconstruct endpoint activity. Correlating Process Creation, Network Connections, File Creation, and DNS Queries provided a complete view of system activity during the investigation.

This workflow reflects a practical SOC investigation process used for endpoint monitoring, threat hunting, and incident response.
