# Network Enumeration

## Objective
Verify connectivity and enumerate the target Windows Server before authentication testing.

## Tool
- NetExec (SMB)

## Command

```bash
netexec smb 192.168.100.10
```

## Findings

- Target IP: 192.168.100.10
- Hostname: WIN-OBNND2CCKKS
- Operating System: Windows Server 2022 Build 20348 x64
- SMB Port: 445/TCP
- SMB Signing: Disabled
- SMBv1: Disabled

## Analyst Notes

The target was successfully identified over SMB. SMB signing is disabled, which is a configuration weakness because it can expose the server to certain relay attacks if other protections are not in place. SMBv1 is disabled, which is considered a security best practice.
