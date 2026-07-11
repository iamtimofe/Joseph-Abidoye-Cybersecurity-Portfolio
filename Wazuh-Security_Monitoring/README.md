# 🔐 Wazuh Security Monitoring & Compliance

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-SIEM%20%2F%20Compliance-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-Monitored%20Host-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-Wazuh-blue?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Completed-green?style=for-the-badge)]()

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Environment](#️-environment)
- [Tools Used](#️-tools-used)
- [Methodology / Steps](#-methodology--steps)
- [Key Findings / Results](#-key-findings--results)
- [Full Report](#-full-report)
- [Lessons Learned](#-lessons-learned)
- [References](#-references)

---

## 🎯 Project Overview

This project uses Wazuh SIEM to monitor a host for integrity violations and ties the resulting
alert back to real-world compliance frameworks. The goal was to move beyond simply "having a SIEM
running" and demonstrate the full workflow of verifying agent health, investigating a live alert,
and explaining why it matters from a compliance standpoint.

### What This Project Demonstrates

- Practical navigation of a SIEM platform beyond the default dashboard
- Understanding of File Integrity Monitoring (FIM) and why checksum mismatches matter
- Ability to connect a technical alert to a business/compliance requirement (PCI DSS, ISO 27001)
- Investigative reasoning determining likely cause and impact of a triggered alert

---

## 🖥️ Environment

| Component        | Details                     |
| ------------------ | ------------------------------ |
| **Platform**        | Wazuh SIEM                     |
| **Monitoring Type**  | Security Events / System Auditing / File Integrity Monitoring |
| **Compliance Scope**  | PCI DSS, ISO 27001              |

---

## 🛠️ Tools Used

| Tool          | Purpose                                          |
| --------------- | --------------------------------------------------- |
| **Wazuh**        | Agent-based monitoring, log analysis, FIM alerting   |

---

## 📐 Methodology / Steps

```
Phase 1: Verify agent connectivity
         ↓
Phase 2: Explore Security Events & System Auditing logs
         ↓
Phase 3: Identify File Integrity Monitoring alert
         ↓
Phase 4: Investigate cause and impact
         ↓
Phase 5: Map finding to compliance frameworks
```

### Phase 1 - Verify Agent Connectivity

**Objective:** Confirm the Wazuh agent is actively reporting before relying on any of its data.

**Result:** Agent connectivity confirmed active and reporting.

### Phase 2 - Explore Logs

**Objective:** Get familiar with the Security Events and System Auditing views to understand what
normal activity looks like on this host.

**Result:** Baseline established for what routine log activity looks like, making the anomaly in
the next phase easier to recognize.

### Phase 3 - Identify FIM Alert

**Objective:** Locate and examine a File Integrity Monitoring alert.

**Result:** Alert identified triggered by a checksum change (SHA1/SHA256 mismatch) on a
monitored file.

### Phase 4 - Investigate

**Objective:** Determine what likely caused the file modification and what the potential impact
is.

**Result:** Investigation traced the change to an unauthorized modification of a monitored file,
consistent with either unauthorized access or a misconfigured process writing where it shouldn't.

### Phase 5 - Compliance Mapping

**Objective:** Tie the FIM alert to the compliance frameworks it's relevant to.

**Result:** Finding mapped to **PCI DSS** (integrity monitoring of critical files/systems) and
**ISO 27001** (Annex A control on information integrity).

---

## 🔍 Key Findings / Results

| Metric                        | Result                                    |
| -------------------------------- | ---------------------------------------------- |
| Alert type                        | File Integrity Monitoring (FIM)                |
| Trigger                           | SHA1/SHA256 checksum mismatch                  |
| Compliance frameworks mapped      | PCI DSS, ISO 27001                             |

**Takeaway:** A File Integrity Monitoring alert is only as useful as the baseline behind it you
need to know which files should never change before a checksum mismatch means anything actionable.

---

## 📊 Full Report

Full screenshots, alert details, and log excerpts are documented in this project's folder in the
main portfolio repository. [Find Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/Wazuh-Security_Monitoring/Security_Monitoring.md)

---

## 📚 Lessons Learned

**1. FIM value depends entirely on baseline accuracy**
An alert is only meaningful if the monitored file list reflects what actually matters monitoring
the wrong files produces noise, not signal.

**2. SIEM navigation is a skill on its own**
Knowing where to look (Security Events vs. System Auditing vs. FIM) matters as much as knowing
what a given alert means once you find it.

**3. Compliance framing turns a technical alert into a business conversation**
Connecting a checksum mismatch to PCI DSS or ISO 27001 requirements is what makes a finding
relevant to people outside the security team.

---

## 📖 References

| Resource                       | URL                                          |
| --------------------------------- | ----------------------------------------------- |
| Wazuh File Integrity Monitoring    | <https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html> |
| PCI DSS Requirements                | <https://www.pcisecuritystandards.org/>          |
| ISO/IEC 27001                       | <https://www.iso.org/standard/27001>              |

---

**⭐ If this project was useful or interesting, please star the repository**

