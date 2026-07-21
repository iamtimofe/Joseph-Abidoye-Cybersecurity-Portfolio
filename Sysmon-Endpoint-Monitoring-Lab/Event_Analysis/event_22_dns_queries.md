# Sysmon Event ID 22 – DNS Query

## Overview

Sysmon Event ID 22 records DNS queries performed by processes running on the endpoint. Unlike standard Windows DNS logs, Sysmon associates each DNS request with the process that initiated it, providing valuable context for threat hunting and incident response.

DNS telemetry is particularly useful for identifying malware beaconing, phishing infrastructure, command-and-control (C2) communications, and suspicious domain lookups.

---

## Lab Objective

The objective of this exercise was to generate DNS queries on a Windows Server 2022 endpoint and analyze the telemetry collected by Microsoft Sysmon.

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

The following command was executed:

```cmd
nslookup github.com
```