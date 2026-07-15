# Event ID 4732 - User Added to Administrators Group

## Overview

This event records the addition of a user account to a privileged local security group.

---

## Event Information

| Field | Value |
|--------|-------|
| Event ID | 4732 |
| Event Name | User Added to Local Administrators Group |
| Group | Administrators |
| User Added | SOC_Analyst |

---

## Analysis

The newly created **SOC_Analyst** account was added to the local **Administrators** group. Membership changes to privileged groups should always be monitored because attackers frequently attempt to escalate privileges after gaining initial access.

---

## SOC Assessment

**Severity:** High

Administrative group membership changes can significantly increase the impact of a security incident if performed without authorization.

---

## Recommendations

- Verify the administrator who performed the action.
- Audit privileged group membership regularly.
- Monitor privileged account activity.
- Enable alerts for future Event ID 4732 occurrences.

---

## MITRE ATT&CK

- T1098 – Account Manipulation
