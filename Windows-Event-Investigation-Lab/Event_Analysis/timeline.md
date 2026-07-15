# Investigation Timeline

| Time | Event ID | Description |
|------|----------|-------------|
| 09:02 | 4625 | Failed local logon |
| 09:05 | 4624 | Successful Administrator logon |
| 09:08 | 4720 | User account "SOC_Analyst" created |
| 09:10 | 4732 | User added to Administrators group |
| 09:22 | 4625 | Failed SMB authentication from 192.168.100.20 |

## Summary

The investigation identified authentication events, account creation, privilege assignment, and simulated remote authentication failures. Correlating these events demonstrates how multiple Windows Security Logs can be combined to reconstruct activity during an investigation.
