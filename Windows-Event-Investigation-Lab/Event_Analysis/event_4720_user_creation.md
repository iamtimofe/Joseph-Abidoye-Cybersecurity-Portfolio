# Event ID 4720 - User Account Creation Investigation

## Overview

This event records the creation of a new local user account on the Windows Server.

---

## Event Information

| Field | Value |
|--------|-------|
| Event ID | 4720 |
| Event Name | User Account Created |
| New Account | SOC_Analyst |
| Created By | Administrator |

---

## Analysis

The Administrator account created a new local user named **SOC_Analyst**. User account creation events are critical because attackers often establish persistence by creating new administrative accounts after compromising a system.

---

## SOC Assessment

**Severity:** Medium

Although this account creation was part of a controlled lab exercise, unauthorized user creation in a production environment should be investigated immediately.

---

## Recommendations

- Verify who created the account.
- Review recent administrative activity.
- Monitor subsequent logon events for the new account.

---

## MITRE ATT&CK

- T1136 – Create Account
