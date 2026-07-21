# Sysmon Event ID 1 – Process Creation

## Overview

Sysmon Event ID 1 records every new process created on a monitored endpoint. Unlike standard Windows logs, Sysmon provides rich telemetry including the executable path, command line, parent process, hashes, user context, and process identifiers.

Process Creation events are one of the most valuable sources of endpoint telemetry for Security Operations Center (SOC) analysts because almost every attack begins with a process execution.

---

## Lab Objective

The objective of this exercise was to generate process creation events on a Windows Server 2022 endpoint and analyze the information captured by Microsoft Sysmon.

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

The following applications were executed to generate Process Creation events:

- Command Prompt (`cmd.exe`)
- Windows PowerShell (`powershell.exe`)
- Google Chrome (`chrome.exe`)
- Notepad (`notepad.exe`)
- Nslookup (`nslookup.exe`)

Sysmon successfully logged each process execution.

---

## Event Summary

| Field | Value |
|-------|-------|
| Event ID | 1 |
| Event Name | Process Creation |
| Log Name | Microsoft-Windows-Sysmon/Operational |
| Severity | Information |

---

## Key Fields Observed

The following information was available in the event:

- Process GUID
- Process ID
- Image
- File Version
- Description
- Company
- Original File Name
- Command Line
- Current Directory
- User
- Logon GUID
- Logon ID
- Terminal Session ID
- Integrity Level
- Hashes (SHA1, SHA256, MD5)
- Parent Process GUID
- Parent Process ID
- Parent Image
- Parent Command Line

---

## Investigation

The event confirmed that Sysmon successfully recorded every new process executed on the endpoint.

Important fields such as the executable path, command line arguments, hashes, parent process, and executing user provide investigators with the ability to reconstruct attacker activity during an incident.

---

## Security Relevance

Event ID 1 is one of the most important Sysmon events because attackers must execute processes to perform malicious actions.

SOC analysts use Process Creation events to detect:

- Malware execution
- PowerShell abuse
- Living-off-the-Land Binaries (LOLBins)
- Command Prompt abuse
- Suspicious parent-child process relationships
- Encoded PowerShell commands
- Script execution
- Privilege escalation attempts

---

## MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1059 | Command and Scripting Interpreter |
| T1204 | User Execution |
| T1106 | Native API |

---

## Detection Opportunities

Security teams should monitor for:

- powershell.exe with Base64 encoded commands
- cmd.exe launched by Microsoft Office
- Browser processes spawning PowerShell
- rundll32.exe executing unusual DLLs
- mshta.exe executing remote content
- regsvr32.exe downloading scripts
- Unusual parent-child process relationships

---

## Lessons Learned

This exercise demonstrated how Sysmon greatly improves endpoint visibility compared to native Windows logging.

The additional telemetry collected by Event ID 1 enables analysts to detect suspicious process execution, investigate malware activity, and perform effective threat hunting.

---

## Conclusion

Process Creation (Event ID 1) provides detailed insight into endpoint activity and serves as the foundation for many threat hunting and incident response investigations.

It is one of the most valuable data sources available to SOC analysts using Microsoft Sysmon.
