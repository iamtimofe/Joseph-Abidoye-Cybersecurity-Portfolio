# Wazuh Security Monitoring – Technical Analysis

## Event Details
- **Agent Name:** Mofe_Windows
- **File Monitored:** `c:\assessment2\joseph_abidoye.txt`
- **Event Type:** File Integrity Monitoring
- **Detection:** Integrity checksum changed
- **Rule ID:** 550
- **Severity Level:** 7
- **Timestamp:** Mar 19, 2026 @ 10:59:02.783
- **Hashes:**
  - SHA1: `0d19dcf4330367ae7c885b38fbc526f940acb955`
  - SHA256: `8a2c0dc6a185bb894f698ae17fab69e8231d3a1a6d975bbcf72c0a30ccd5df60`

---

## Technical Explanation
The Wazuh agent detected a modification in the file `joseph_abidoye.txt`.  
This was identified because the cryptographic hash values (SHA1/SHA256) no longer matched the baseline stored in Wazuh’s database.  
Such changes trigger a **checksum mismatch alert**, which is logged with severity level 7.

---

## Compliance Relevance
File Integrity Monitoring (FIM) is a requirement in several compliance frameworks:
- **PCI DSS Requirement 11.5** – Deploy file integrity monitoring tools to alert personnel to unauthorized modification of critical system files.
- **ISO 27001 A.12.2.1** – Controls to detect unauthorized changes to software and information.
- **HIPAA Security Rule** – Ensures integrity of electronic protected health information (ePHI).

By detecting unauthorized modifications, organizations can:
- Prevent insider threats
- Detect malware persistence
- Maintain audit trails for compliance

---

## Reflection
This event demonstrates how SIEM tools like Wazuh provide visibility into system changes.  
By correlating alerts with compliance requirements, security teams can both **strengthen defenses** and **prove adherence to standards** during audits.
