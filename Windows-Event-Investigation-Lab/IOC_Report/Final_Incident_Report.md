# Windows Security Event Investigation Report

## Executive Summary

A Windows Server 2022 host was investigated following simulated security events, including failed logon attempts, successful authentication, user account creation, privilege escalation, and remote SMB authentication failures. The objective was to analyze Windows Security Event Logs, identify indicators of suspicious activity, and document findings using SOC investigation methodology.

---

## Scope

- Windows Server 2022
- Kali Linux (Attack Simulation)
- Event Viewer
- NetExec
- Nmap

---

## Investigation Timeline

| Phase | Event ID | Description |
|---------|----------|-------------|
| Phase 1 | 4625 | Failed Local Logon |
| Phase 2 | 4624 | Successful Logon |
| Phase 3 | 4720 | User Account Created |
| Phase 4 | 4732 | User Added to Administrators Group |
| Phase 5 | 4625 | Failed SMB Authentication |

---

## Key Findings

- Detected failed authentication attempts.
- Identified successful logon events.
- Verified creation of a new local user account.
- Confirmed privileged group membership modification.
- Simulated remote authentication failures from Kali Linux.
- Correlated security events with network activity.

---

## MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Valid Accounts | T1078 |
| Account Manipulation | T1098 |
| Brute Force | T1110 |
| Password Guessing | T1110.001 |

---

## Skills Demonstrated

- Windows Event Log Analysis
- Incident Investigation
- IOC Collection
- Network Enumeration
- SMB Authentication Analysis
- Security Documentation
- Threat Detection
- SOC Reporting

---

## Conclusion

This investigation demonstrates a structured Security Operations Center (SOC) workflow for detecting, analyzing, and documenting Windows authentication events and privilege changes. The lab highlights practical blue-team skills in log analysis, attack simulation, event correlation, and incident reporting.
