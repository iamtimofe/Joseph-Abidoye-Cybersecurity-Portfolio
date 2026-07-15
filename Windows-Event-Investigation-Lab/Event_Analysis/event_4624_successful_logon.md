# Event ID 4624 - Successful Logon Investigation

## Overview

This event records a successful authentication to the Windows Server.

---

## Event Information

| Field | Value |
|--------|-------|
| Event ID | 4624 |
| Event Name | Successful Logon |
| Logon Type | Interactive |
| Target Account | Administrator |

---

## Analysis

The event indicates that the Administrator account successfully authenticated to the Windows Server. Successful logon events should always be correlated with previous failed logon attempts to determine whether unauthorized access occurred after repeated authentication failures.

---

## SOC Assessment

**Severity:** Informational

This event is expected during normal administrative activity. However, repeated successful logons following multiple failed authentication attempts should be investigated for potential brute-force attacks.

---

## Recommendations

- Correlate with Event ID 4625.
- Verify the legitimacy of the user.
- Review the logon timeline for suspicious patterns.

---

## MITRE ATT&CK

- T1078 – Valid Accounts
