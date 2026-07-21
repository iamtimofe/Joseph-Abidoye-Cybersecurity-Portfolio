# 🛡️ Sysmon Endpoint Monitoring & Threat Hunting Lab

<p align="center">

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-blue?style=for-the-badge&logo=windows)
![Sysmon](https://img.shields.io/badge/Microsoft-Sysmon-red?style=for-the-badge&logo=microsoft)
![Threat Hunting](https://img.shields.io/badge/Threat-Hunting-success?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Analyst-blueviolet?style=for-the-badge)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-orange?style=for-the-badge)

</p>

---

## 📖 Executive Summary

This project demonstrates how Microsoft Sysmon can be deployed to enhance endpoint visibility on a Windows Server 2022 system.

Unlike default Windows logging, Sysmon records detailed telemetry about process execution, network connections, DNS activity, and file creation, making it one of the most valuable tools for Security Operations Centers (SOC), Incident Response (IR), Digital Forensics (DFIR), and Threat Hunting.

During this lab, Microsoft Sysmon was installed using the SwiftOnSecurity configuration. Multiple endpoint activities were intentionally generated and analyzed through Event Viewer to simulate a real-world SOC investigation.

The project documents the investigation process, collected evidence, Indicators of Compromise (IOCs), and the techniques used to identify and analyze endpoint activity.

---

## 🎯 Objectives

The primary objectives of this lab were to:

- Deploy Microsoft Sysmon on Windows Server 2022
- Configure enhanced endpoint logging
- Generate realistic endpoint telemetry
- Analyze Sysmon Operational logs
- Investigate Process Creation events
- Investigate Network Connection events
- Investigate File Creation events
- Investigate DNS Query events
- Collect Indicators of Compromise (IOCs)
- Document findings using industry-standard investigation reports

---

## 🏗️ Lab Architecture

```text
                    +----------------------+
                    |  Kali Linux Analyst  |
                    |  Investigation Notes |
                    +----------+-----------+
                               |
                               |
                        Event Investigation
                               |
                               ▼
+-----------------------------------------------------------+
|              Windows Server 2022 Endpoint                 |
|-------------------------------------------------------------|
|                                                             |
|  Microsoft Sysmon                                          |
|                                                             |
|   • Event ID 1  - Process Creation                         |
|   • Event ID 3  - Network Connection                       |
|   • Event ID 11 - File Creation                            |
|   • Event ID 22 - DNS Queries                               |
|                                                             |
+-------------------------------------------------------------+
```

---

## 🔍 Event Analysis

The following Sysmon events were generated, collected, and analyzed during this investigation.

| Event ID | Event | Description | Report |
|----------|-------|-------------|--------|
| 1 | Process Creation | Records newly created processes including command line, hashes, and parent process information. | [event_1_process_creation.md](Event_Analysis/event_1_process_creation.md) |
| 3 | Network Connection | Records outbound TCP/UDP network connections initiated by processes. | [event_3_network_connection.md](Event_Analysis/event_3_network_connection.md) |
| 11 | File Creation | Records files created on the endpoint, including downloaded files and alternate data streams. | [event_11_file_creation.md](Event_Analysis/event_11_file_creation.md) |
| 22 | DNS Query | Records DNS lookups and associates them with the originating process. | [event_22_dns_queries.md](Event_Analysis/event_22_dns_queries.md) |

Additional documentation:

- 📄 [Event Summary](Event_Analysis/event_summary.md)
- ⏱️ [Investigation Timeline](Event_Analysis/timeline.md)

---

## 📑 Indicators of Compromise (IOCs)

The investigation collected multiple Indicators of Compromise that can be used during threat hunting and incident response.

Examples include:

- Process Names
- Process GUIDs
- Process IDs
- Parent Processes
- Command Lines
- File Paths
- DNS Queries
- Destination IP Addresses
- User Accounts
- UTC Timestamps

Complete IOC list:

➡️ **[IOC Report](IOC_Report/iocs.txt)**

Final investigation report:

➡️ **[Final Incident Report](IOC_Report/Final_Incident_Report.md)**

---

## 🖼️ Evidence & Screenshots

The following screenshots document each stage of the investigation.

| Screenshot | Description |
|------------|-------------|
| `01_process_creation.png` | Sysmon Event ID 1 – Process Creation |
| `02_network_connection.png` | Sysmon Event ID 3 – Network Connection |
| `03_file_creation.png` | Sysmon Event ID 11 – File Creation |
| `04_dns_query.png` | Sysmon Event ID 22 – DNS Query |

> All screenshots are located in the `Screenshots/` directory.

---

## 🧩 MITRE ATT&CK Mapping

| Sysmon Event | ATT&CK Technique | Description |
|--------------|------------------|-------------|
| Event ID 1 | T1059 | Command and Scripting Interpreter |
| Event ID 3 | T1071 | Application Layer Protocol |
| Event ID 11 | T1105 | Ingress Tool Transfer |
| Event ID 22 | T1071.004 | Application Layer Protocol: DNS |

---

## 📈 Investigation Summary

The investigation confirmed that Microsoft Sysmon successfully captured endpoint telemetry across multiple categories of activity.

### Successfully Validated

- ✅ Process Creation Monitoring
- ✅ Network Connection Monitoring
- ✅ File Creation Monitoring
- ✅ DNS Query Monitoring

### Security Benefits

- Improved endpoint visibility
- Faster incident investigation
- Enhanced threat hunting capability
- Better IOC collection
- Rich endpoint telemetry for SIEM ingestion

---

## 📊 Skills Demonstrated During This Lab

- Windows Endpoint Monitoring
- Sysmon Deployment & Configuration
- Event Log Analysis
- Process Investigation
- Network Traffic Analysis
- DNS Investigation
- File System Monitoring
- Threat Hunting
- IOC Collection
- Incident Documentation
- MITRE ATT&CK Mapping
- Technical Report Writing

---

## 🚧 Challenges Encountered

During this lab, several technical challenges were encountered while configuring and validating Sysmon.

| Challenge | Resolution |
|-----------|------------|
| Event ID 11 (File Creation) was not appearing | Verified the Sysmon configuration included FileCreate events and generated a new file creation event by downloading the Sysmon configuration file. |
| Network connectivity issues in the Windows Server VM | Restored the VM networking configuration and confirmed Internet access before continuing the lab. |
| Incorrect Sysmon executable location | Moved the Sysmon files to `C:\Sysmon` and completed the installation from the correct directory. |
| Event validation | Verified generated events in **Applications and Services Logs → Microsoft → Windows → Sysmon → Operational** using Event Viewer. |

---

## 📚 Lessons Learned

This project reinforced several key SOC analyst concepts:

- Endpoint visibility is significantly improved with Sysmon compared to default Windows logging.
- Process execution, network activity, file creation, and DNS queries can be correlated to reconstruct endpoint activity.
- Proper Sysmon configuration is essential for collecting useful telemetry.
- Documentation is a critical part of every investigation and should clearly explain findings and evidence.

---

## 🚀 Future Improvements

This project will be expanded by integrating Sysmon logs into additional security platforms and creating custom detections.

Planned enhancements include:

- Integrate Sysmon with **Wazuh SIEM**
- Forward logs to **Splunk**
- Create **Sigma detection rules**
- Convert Sigma rules to **Splunk SPL** and **Wazuh rules**
- Build custom threat hunting queries
- Simulate malware execution in a safe lab environment
- Create additional investigations covering persistence, privilege escalation, and lateral movement

---

## 👨🏽‍💻 Author

**Joseph Abidoye**

Aspiring SOC Analyst with a strong focus on:

- Security Operations (SOC)
- Endpoint Monitoring
- Threat Hunting
- Windows Security
- Active Directory
- Network Security
- SIEM Technologies
- Incident Response

### Connect with Me

- GitHub: **https://github.com/iamtimofe**

---

## ⭐ Key Takeaways

This project demonstrates practical experience with:

- Microsoft Sysmon deployment
- Windows endpoint monitoring
- Security event analysis
- Threat hunting techniques
- IOC identification
- MITRE ATT&CK mapping
- Incident documentation
- Technical reporting

The investigation follows a structured workflow similar to that used by Security Operations Center (SOC) analysts during endpoint investigations and incident response.

---

## 🏛️ NIST Cybersecurity Framework Mapping

This project aligns with the NIST Cybersecurity Framework (CSF) 2.0 by demonstrating practical endpoint monitoring, detection, and incident analysis.

| Function | Application in this Project |
|----------|-----------------------------|
| Identify | Understanding endpoint telemetry collected by Sysmon |
| Protect | Deploying and configuring Microsoft Sysmon |
| Detect | Monitoring process creation, network connections, DNS queries, and file creation events |
| Respond | Investigating security events, collecting IOCs, and documenting findings |
| Recover | Not covered in this lab |

**Primary NIST CSF Function:** **Detect (DE)**

Relevant categories include:

- **DE.CM – Security Continuous Monitoring**
- **DE.AE – Adverse Event Analysis**
- **RS.AN – Incident Analysis**
- **PR.PS – Platform Security**
