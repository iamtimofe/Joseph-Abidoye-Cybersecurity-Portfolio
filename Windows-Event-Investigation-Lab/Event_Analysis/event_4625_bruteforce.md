# Event ID 4625 - Failed Network Logon Investigation

## Incident Summary

A simulated brute-force authentication attempt was performed from a Kali Linux system against a Windows Server 2022 host using SMB authentication.

## Event Details

| Field | Value |
|-------|-------|
| Event ID | 4625 |
| Logon Type | 3 (Network) |
| Source IP | 192.168.100.20 |
| Target Account | Administrator |
| Authentication Package | NTLM |
| Failure Reason | Unknown user name or bad password |
| Status | 0xC000006D |
| Sub Status | 0xC000006A |

## Analysis

The failed authentication originated from the Kali Linux attack host over SMB. The use of incorrect credentials resulted in Windows generating Event ID 4625. Multiple failed authentication attempts from the same source IP could indicate a brute-force or password-spraying attack.

## MITRE ATT&CK

- T1110 – Brute Force
- T1110.001 – Password Guessing
- T1078 – Valid Accounts (Attempted)

## Recommendations

- Monitor repeated failed logons.
- Correlate Event ID 4625 with Event ID 4624.
- Implement account lockout policies.
- Investigate repeated authentication attempts against privileged accounts.
