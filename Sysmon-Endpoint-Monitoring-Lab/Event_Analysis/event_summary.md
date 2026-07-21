# Sysmon Event Summary

## Executive Summary

This investigation demonstrates how Microsoft Sysmon enhances Windows endpoint visibility by capturing detailed telemetry that is not available through default Windows Event Logs.

During this lab, multiple activities were intentionally performed to generate Sysmon events for analysis. These events were reviewed using Event Viewer and documented to simulate a Security Operations Center (SOC) investigation.

---

## Events Investigated

| Event ID | Event Name | Purpose |
|----------|------------|---------|
| 1 | Process Creation | Records newly created processes |
| 3 | Network Connection | Records outbound network connections |
| 11 | File Creation | Records files created on disk |
| 22 | DNS Query | Records DNS lookups performed by processes |

---

## Key Findings

### Event ID 1 – Process Creation

- Captured execution of Windows processes.
- Recorded parent-child process relationships.
- Logged command-line arguments and process hashes.

---

### Event ID 3 – Network Connection

- Recorded outbound network activity.
- Identified the originating process.
- Logged destination IP addresses and ports.

---

### Event ID 11 – File Creation

- Captured the creation of downloaded files.
- Recorded the process responsible for writing the file.
- Detected creation of the Zone.Identifier Alternate Data Stream.

---

### Event ID 22 – DNS Query

- Recorded DNS lookups performed by running processes.
- Associated DNS requests with the originating process.
- Logged query names and query results.

---

## Security Value

Together, these events provide comprehensive endpoint visibility and support:

- Threat Hunting
- Malware Detection
- Incident Response
- Digital Forensics
- IOC Collection
- Endpoint Monitoring

---

## Conclusion

Sysmon significantly improves endpoint monitoring by recording detailed process, network, file, and DNS activity.

These logs provide valuable telemetry for SOC analysts to detect suspicious behavior, investigate incidents, and identify attacker techniques.
