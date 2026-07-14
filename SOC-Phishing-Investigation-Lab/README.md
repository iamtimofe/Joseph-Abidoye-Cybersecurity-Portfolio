# 🛡️ SOC Phishing Investigation Lab

## 📌 Project Overview

This project documents a phishing investigation conducted in a Kali Linux virtual machine as part of my cybersecurity training. The objective was to investigate a live phishing website, collect indicators of compromise (IOCs), perform threat intelligence enrichment, and document the findings in a professional incident report.

---

## 🎯 Objectives

- Investigate a reported phishing website
- Collect Indicators of Compromise (IOCs)
- Perform DNS and WHOIS analysis
- Analyze HTTP response headers
- Perform IP reputation checks
- Produce a professional investigation report

---

## 🛠️ Tools Used

- Kali Linux
- Oracle VirtualBox
- PhishTank
- VirusTotal
- IPinfo
- AbuseIPDB
- dig
- whois
- curl

---

## 🔍 Investigation Workflow

1. Identified the phishing URL from PhishTank.
2. Verified the URL using VirusTotal.
3. Performed DNS enumeration.
4. Collected WHOIS and infrastructure information.
5. Analyzed HTTP response headers.
6. Performed IP reputation analysis.
7. Documented all findings in an investigation report.

---

## 📊 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Domain | `bbgoverno.digital` |
| IP Address | `5.230.71.248` |
| Nameservers | `ns1.dyna-ns.net`, `ns2.dyna-ns.net` |

---

## 📝 Key Findings

- The phishing website was active during the investigation.
- The domain resolved to **5.230.71.248**.
- Infrastructure was hosted by **GHOSTnet GmbH** in Germany.
- VirusTotal identified the URL as phishing.
- DNS and HTTP analysis supported the phishing assessment.

---

## 🛡️ MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
| Initial Access | T1566.002 – Phishing: Link |
| Resource Development | T1583 – Acquire Infrastructure |

---

## 📂 Project Contents

- `Evidence/` – Investigation notes
- `IOC_Report/` – Final report and collected IOCs
- `WHOIS/` – DNS, WHOIS and HTTP analysis
- `Screenshots/` – Evidence screenshots
- `URL_Analysis/` – URL analysis files

---

## 💡 Skills Demonstrated

- Phishing Investigation
- Threat Intelligence
- IOC Collection
- DNS Analysis
- WHOIS Analysis
- HTTP Header Analysis
- Linux Command Line
- Documentation
- Incident Reporting

---

## ⚠️ Disclaimer

This project was completed in a controlled lab environment for educational purposes. No unauthorized access, exploitation, or interaction beyond passive analysis was performed.
