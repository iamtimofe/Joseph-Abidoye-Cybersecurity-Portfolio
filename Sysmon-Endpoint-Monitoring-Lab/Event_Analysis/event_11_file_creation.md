# Sysmon Event ID 11 – File Creation

## Overview

Sysmon Event ID 11 records files created on a monitored endpoint. It provides detailed visibility into applications writing files to disk, making it a valuable source of telemetry for detecting malware payloads, ransomware activity, unauthorized downloads, and persistence mechanisms.

Unlike standard Windows logging, Sysmon identifies the exact process responsible for creating a file, enabling analysts to trace suspicious activity back to its source.

---

## Lab Objective

The objective of this exercise was to generate File Creation events and analyze the telemetry recorded by Microsoft Sysmon.

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

During the lab, the Sysmon configuration file was downloaded using Google Chrome.

Windows automatically created a **Zone.Identifier Alternate Data Stream (ADS)**, commonly referred to as the **Mark of the Web (MOTW)**.

Sysmon successfully recorded this file creation activity.

---

## Event Summary

| Field | Value |
|-------|-------|
| Event ID | 11 |
| Event Name | File Create |
| Log Name | Microsoft-Windows-Sysmon/Operational |
| Severity | Information |

---

## Key Fields Observed

The following information was available in the event:

- Process GUID
- Process ID
- Image
- User
- Target Filename
- Rule Name
- UTC Time

---

## Investigation

The event identified **Google Chrome** as the process responsible for creating the file.

**Process**

```text
C:\Program Files\Google\Chrome\Application\chrome.exe
```
**Target File**

```text
C:\Users\Administrator\Downloads\sysmonconfig-export.xml:Zone.Identifier
```
