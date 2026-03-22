# Wazuh Security Monitoring and Compliance

## Scenario
Utilizing a Security Information and Event Management (SIEM) tool is critical for real-time threat detection.  
This project demonstrates how Wazuh can be used to identify and analyze security events.

## Tasks
1. **Access Dashboard**  
   Logged into Wazuh dashboard via lab environment. Verified agent connectivity.

2. **Log Exploration**  
   Navigated to *Security Events* and *System Auditing* tabs. Observed alerts categorized by severity.

3. **Event Identification**  
   Selected alert: *File Integrity Monitoring — Integrity checksum changed for `c:\assessment2\joseph_abidoye.txt`.*

4. **Analysis**  
   - **Technical Explanation:** Wazuh detected a modification in the file’s cryptographic hash (SHA1/SHA256 mismatch).  
   - **Importance:** File integrity monitoring is critical for compliance frameworks (e.g., PCI DSS, ISO 27001). Detecting unauthorized changes helps prevent insider threats, malware persistence, and data tampering.

## Security Event Summary
- **Event Type:** File Integrity Monitoring  
- **File:** `c:\assessment2\joseph_abidoye.txt`  
- **Detection:** Integrity checksum changed (Rule ID 550, Severity Level 7)  
- **Compliance Relevance:** Supports PCI DSS Requirement 11.5 — “Deploy file integrity monitoring tools to alert personnel to unauthorized modification of critical system files.”

## Reflection
This exercise demonstrates how SIEM tools like Wazuh provide visibility into system changes, enabling proactive compliance and threat detection.
