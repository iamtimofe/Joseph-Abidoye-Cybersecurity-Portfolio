# Phishing Investigation Report

**Investigator:** Folayinka

**Role:** SOC Analyst (Lab)

**Case ID:** CASE-001

**Date:** July 14, 2026

---

# Executive Summary

A phishing URL hosted on the domain **bbgoverno.digital** was investigated following its identification on PhishTank.

The investigation confirmed that the website was online, redirected users to a phishing landing page, and had already been detected as phishing by ESET on VirusTotal.

DNS analysis, HTTP response analysis, IP intelligence, and infrastructure enrichment were performed to determine the characteristics of the phishing infrastructure.

---

# Scope

The investigation focused on:

- Domain analysis
- DNS investigation
- Threat intelligence
- Infrastructure analysis
- IOC collection
- Reputation analysis

---

# Investigation Timeline

| Phase | Activity |
|--------|----------|
| 1 | Collected phishing URL from PhishTank |
| 2 | Performed DNS investigation |
| 3 | Conducted VirusTotal analysis |
| 4 | Investigated infrastructure |
| 5 | Enumerated DNS records |
| 6 | Collected Indicators of Compromise |
| 7 | Analyzed HTTP headers |
| 8 | Performed IP intelligence enrichment |
| 9 | Checked AbuseIPDB reputation |

---

# Indicators of Compromise

## Domain

bbgoverno.digital

---

## URL

hxxps://bbgoverno[.]digital/appcx/index.html

---

## IP Address

5.230.71.248

---

## Name Servers

ns1.dyna-ns.net

ns2.dyna-ns.net

---

# DNS Findings

| Record | Result |
|---------|--------|
| A | 5.230.71.248 |
| AAAA | None |
| MX | None |
| TXT | None |

---

# VirusTotal Findings

Detection Ratio:

1 / 92

Detected By:

- ESET (Phishing)

Observations:

- Website active
- HTTP Status 200
- HTML content served

---

# HTTP Analysis

The server returned:

HTTP/2 302

Redirect Location:

appcx/index.html

Observed Headers:

- nginx
- PHPSESSID cookie
- cookie_test cookie
- HSTS enabled
- Cache disabled

---

# Infrastructure Intelligence

Country:

Germany

City:

Frankfurt am Main

Hosting Provider:

GHOSTnet GmbH

ASN:

AS12586

Usage Type:

Data Center / Web Hosting

---

# Abuse Intelligence

AbuseIPDB Score:

0%

Reports:

0

Assessment:

Although AbuseIPDB contained no reports for the IP address, multiple independent sources identified the associated URL as phishing. The lack of abuse reports likely reflects the recent deployment of the infrastructure rather than an absence of malicious activity.

---

# Technical Assessment

The investigation identified several characteristics commonly associated with phishing infrastructure:

- Active phishing landing page
- URL publicly reported by PhishTank
- Detection by ESET on VirusTotal
- Redirect to phishing content
- PHP session management
- VPS-hosted infrastructure
- No email infrastructure
- No IPv6 configuration

---

# Risk Assessment

Risk Level:

HIGH

Reason:

The phishing website was operational and capable of serving phishing content to victims.

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Phishing | T1566 |
| Phishing Link | T1566.002 |
| Acquire Infrastructure | T1583 |
| Web Service | T1583.006 |

---

# Recommendations

- Block the domain:

bbgoverno.digital

- Block IP:

5.230.71.248

- Notify users who may have accessed the phishing page.

- Monitor DNS and firewall logs for connections to the domain.

- Continue monitoring threat intelligence feeds for additional indicators.

---

# Lessons Learned

This investigation demonstrated how multiple intelligence sources should be correlated before reaching a conclusion.

Although AbuseIPDB contained no reports, PhishTank, VirusTotal, DNS analysis, and HTTP analysis collectively indicated phishing activity.

Threat intelligence should always be evaluated using multiple independent sources rather than relying on a single reputation service.

---

# Skills Demonstrated

- Linux
- Kali Linux
- DNS Investigation
- Threat Intelligence
- VirusTotal
- PhishTank
- HTTP Analysis
- IOC Collection
- OSINT
- Incident Documentation
- MITRE ATT&CK Mapping
- SOC Investigation Workflow
