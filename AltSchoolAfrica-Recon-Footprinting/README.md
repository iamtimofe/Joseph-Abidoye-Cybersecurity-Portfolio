# 🔐 External Reconnaissance & Attack Surface Mapping

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-OSINT%20%2F%20Recon-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-Authorized%20Lab%20Domain-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-Amass%20%7C%20Nmap-blue?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Completed-green?style=for-the-badge)]()

---

> **⚠️ Legal Disclaimer:** This reconnaissance engagement was conducted against a domain
> explicitly authorized for coursework testing, as part of an AltSchool Africa assessnment. No
> unauthorized targets were scanned or enumerated. All findings are documented for educational
> purposes only.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Environment](#️-environment)
- [Tools Used](#️-tools-used)
- [Methodology / Steps](#-methodology--steps)
- [Key Findings / Results](#-key-findings--results)
- [Lessons Learned](#-lessons-learned)
- [Full Report](#-full-report)
- [References](#-references)

---

## 🎯 Project Overview

This project runs a full external reconnaissance and footprinting engagement against an
authorized lab domain, combining passive OSINT with active Nmap scanning to map its real attack
surface the same first phase a real penetration test or red team engagement would begin with.

### What This Project Demonstrates

- Structured passive OSINT methodology using multiple complementary tools
- Active scanning discipline host discovery before deep enumeration
- Ability to interpret scan output into real infrastructure insight (e.g. CDN detection, SAN leaks)
- Translating raw findings into a risk-ranked target list and visual attack surface map

---

## 🖥️ Environment

| Component        | Details                          |
| ------------------ | ------------------------------------ |
| **Attacker OS**       | Kali Linux                            |
| **Target**             | Authorized lab domain (AltSchool Africa coursework) |
| **Testing Type**       | Black-box, passive-first methodology  |

---

## 🛠️ Tools Used

| Tool                | Purpose                                             |
| --------------------- | -------------------------------------------------------- |
| **Amass**               | Subdomain enumeration and asset discovery                  |
| **Recon-ng**             | OSINT reconnaissance framework                              |
| **theHarvester**         | Email/subdomain/host harvesting from public sources          |
| **WHOIS / dig**          | Domain registration and DNS record lookups                    |
| **Google Dorking**       | Manual search-engine-based reconnaissance                     |
| **Nmap**                 | Active host discovery and port/service scanning               |
| **draw.io**              | Attack surface / Data Flow Diagram documentation               |

---

## 📐 Methodology / Steps

```
Phase 1: Scope definition
         ↓
Phase 2: Passive OSINT collection
         ↓
Phase 3: Active host discovery
         ↓
Phase 4: Port and service scanning
         ↓
Phase 5: Attack surface mapping & documentation
```

### Phase 1 - Scope Definition

**Objective:** Formally define what's in scope before any tool is run.

**Result:** Target domain confirmed as the sole in-scope asset; all activity restricted to that
domain and its resolved infrastructure.

### Phase 2 - Passive OSINT

**Objective:** Gather as much information as possible without sending a single packet directly to
the target's infrastructure.

```
amass enum -d target-domain.com
theHarvester -d target-domain.com -b all
whois target-domain.com
dig target-domain.com ANY
```

**Result:** Subdomains, DNS records, and publicly indexed information collected including
confirmation that the domain sits behind Cloudflare.

### Phase 3 - Active Host Discovery

**Objective:** Confirm which resolved hosts are actually live before deeper scanning.

```
nmap -sn target-domain.com
```

**Result:** Live hosts confirmed, ready for port/service enumeration.

### Phase 4 - Port & Service Scanning

**Objective:** Identify open ports and running services on the confirmed live hosts.

```
nmap -sV -A target-domain.com
```

**Result:** Four open TCP ports identified on a Cloudflare edge node. Certificate inspection
revealed an SSL SAN field disclosing a subdomain not found through passive enumeration alone.

### Phase 5 - Attack Surface Mapping

**Objective:** Convert raw findings into a structured, risk-ranked view of the target's exposure.

**Result:** Findings compiled into a risk-ranked target list and a Data Flow Diagram (built in
draw.io) visualizing the discovered attack surface.

---

## 🔍 Key Findings / Results

| Finding                                   | Detail                                          |
| -------------------------------------------- | ------------------------------------------------- |
| CDN / WAF in front of target                  | Cloudflare confirmed                              |
| Open TCP ports (edge node)                     | 4 open ports identified                            |
| Information disclosure                         | SSL certificate SAN field leaked a hidden subdomain |
| Documentation output                           | Risk-ranked target list + attack surface DFD       |

**Takeaway:** A surprising amount of real infrastructure detail can be inferred from public,
passive sources alone — and a single SSL certificate SAN field turned out to be more informative
than the entire passive subdomain enumeration phase.

---

## 📊 Full Report

Full tool output, screenshots, and the attack surface diagram are documented in this project's
folder in the main portfolio repository. - [Read Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/AltSchoolAfrica-Recon-Footprinting/External%20Reconnaissance%20%26%20Attack%20Surface%20Mapping%20%20AltSchoolAfrica.md)

---

## 📚 Lessons Learned

**1. Passive recon punches above its weight**
A meaningful picture of the target's infrastructure was built before a single active scan was
run a reminder of how much organizations expose without realizing it.

**2. Certificates leak more than they're meant to**
The SSL SAN field disclosure was the single highest-value finding of the engagement, despite
coming from a completely passive, non-intrusive check.

**3. CDNs complicate but don't eliminate reconnaissance**
Cloudflare fronting the target meant the "visible" IP wasn't the real origin server, which shaped
how findings had to be interpreted and documented.

---

## 📖 References

| Resource                | URL                                          |
| --------------------------- | ------------------------------------------------ |
| OWASP Testing Guide — Recon   | <https://owasp.org/www-project-web-security-testing-guide/> |
| Amass                        | <https://github.com/owasp-amass/amass>              |
| theHarvester                 | <https://github.com/laramies/theHarvester>          |

---

**⭐ If this project was useful or interesting, please star the repository**

