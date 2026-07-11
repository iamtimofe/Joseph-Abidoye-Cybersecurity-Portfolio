# 🔐 Web Application Vulnerabilities — DVWA

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-Web%20Application%20Security-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-DVWA-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-Burp%20Suite-blue?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Completed-green?style=for-the-badge)]()

---

> **⚠️ Legal Disclaimer:** This assessment was conducted entirely against Damn Vulnerable Web
> Application (DVWA), a deliberately vulnerable application designed for security training,
> deployed in an isolated local lab environment. No real production systems or third-party
> applications were targeted. All findings are documented for educational purposes only.

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

This project simulates a web application security assessment for a fictional fintech (CyberFin
Labs), targeting DVWA to identify and exploit OWASP Top 10 vulnerabilities. The goal was to
produce a professional, developer-facing findings report not just prove exploitability, but
explain severity, evidence, and concrete remediation for each issue.

### What This Project Demonstrates

- Practical exploitation of SQL Injection, Reflected XSS, and CSRF
- Proficiency with Burp Suite for request interception and manipulation
- Ability to map raw findings to the OWASP Top 10 with severity ratings
- Developer-facing remediation writing, not just "found a bug" reporting

---

## 🖥️ Environment

| Component        | Details                          |
| ------------------ | ------------------------------------ |
| **Target**           | DVWA (Damn Vulnerable Web Application) |
| **Attacker OS**       | Kali Linux                            |
| **Proxy**             | Burp Suite Pro                        |
| **Security Level**    | Low → Medium (DVWA setting)           |

---

## 🛠️ Tools Used

| Tool                | Purpose                                       |
| --------------------- | -------------------------------------------------- |
| **DVWA**               | Intentionally vulnerable target application         |
| **Burp Suite Pro**      | Request interception, repeater, manual manipulation |
| **Kali Linux**          | Attacking platform                                   |

---

## 📐 Methodology / Steps

```
Phase 1: Recon the DVWA application surface
         ↓
Phase 2: Exploit SQL Injection
         ↓
Phase 3: Exploit Reflected XSS
         ↓
Phase 4: Exploit CSRF
         ↓
Phase 5: Map findings to OWASP Top 10 & write remediation
```

### Phase 1 - Application Recon

**Objective:** Identify DVWA's input points (login, search, forms) as candidate attack surfaces.

**Result:** SQLi, XSS, and CSRF entry points identified across the DVWA module set.

### Phase 2 - SQL Injection

**Objective:** Exploit the SQLi module using UNION-based payloads via Burp Suite.

```
' UNION SELECT user, password FROM users -- -
```

**Result:** Extracted password hashes from the backend database and cracked them offline,
confirming full database read access via injection.

### Phase 3 — Reflected XSS

**Objective:** Confirm reflected XSS in an unsanitized input field.

```html
<script>alert('XSS')</script>
```

**Result:** JavaScript payload executed in the browser context, confirming the application
reflects unsanitized user input directly into the page.

### Phase 4 - CSRF

**Objective:** Build a forged HTML page that triggers a state-changing action (password change)
with no victim interaction required.

**Result:** Forged page successfully changed a victim's password with zero interaction beyond
visiting the malicious page while authenticated to DVWA.

### Phase 5 - Mapping & Remediation

**Objective:** Formally classify each finding against OWASP Top 10 and write a fix for each.

**Result:** All three findings mapped, rated, and paired with code-level remediation guidance.

---

## 🔍 Key Findings / Results

| ID       | Finding                    | Severity   | OWASP Top 10 Category                    |
| -------- | ----------------------------- | ---------- | ---------------------------------------- |
| WEB-01   | SQL Injection (UNION-based)    | 🔴 Critical | A03:2021 - Injection                     |
| WEB-02   | Reflected Cross-Site Scripting | 🟠 High     | A03:2021 - Injection                     |
| WEB-03   | Cross-Site Request Forgery     | 🟠 High     | A01:2021 - Broken Access Control          |

### WEB-01 - SQL Injection

**Description:** The login/search input fields fail to sanitize user input, allowing UNION-based
injection to read arbitrary tables from the backend database.

**Evidence:** Extracted and cracked password hashes via Burp Suite-assisted injection.

**Impact:** Full database read access complete compromise of user credential data.

**Remediation:** Use parameterized queries / prepared statements exclusively; never concatenate
user input into SQL strings.

### WEB-02 - Reflected XSS

**Description:** User-supplied input is reflected into the page without output encoding, allowing
arbitrary JavaScript execution in the victim's browser.

**Evidence:** `<script>alert('XSS')</script>` payload executed successfully.

**Impact:** Session hijacking, credential theft, or arbitrary actions performed as the victim.

**Remediation:** Apply context-aware output encoding on all reflected input; implement a
Content-Security-Policy header.

### WEB-03 - CSRF

**Description:** State-changing endpoints (e.g. password change) lack anti-CSRF tokens, allowing
a forged external page to trigger the action on behalf of an authenticated victim.

**Evidence:** Forged HTML page silently changed a logged-in victim's password.

**Impact:** Account takeover without the victim ever entering their credentials to the attacker.

**Remediation:** Implement per-session anti-CSRF tokens on all state-changing requests; validate
`Origin`/`Referer` headers as a secondary control.

---

## 📊 Full Report

Full payload details, Burp Suite request/response evidence, and screenshots are documented in this
project's folder in the main portfolio repository. - [Full Reports](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/Web-Application-Vulnerabilities-DVWA/Web-App%20Vulnerability.md)

---

## 📚 Lessons Learned

**1. Unvalidated input is the root of most web vulnerabilities**
All three findings — despite being different vulnerability classes trace back to the same root
cause: user input trusted without validation or encoding.

**2. Exploitability and severity aren't always the same thing**
CSRF required no complex payload at all, just the absence of a token, a reminder that "simple to
exploit" doesn't mean "low severity."

**3. A finding without a fix isn't a complete report**
Producing remediation guidance alongside each exploit, not just proof it worked, is what makes a
report usable by a development team.

---


## 📖 References

| Resource                    | URL                                                        |
| ------------------------------ | -------------------------------------------------------------- |
| OWASP Top 10 (2021)             | <https://owasp.org/Top10/>                                      |
| DVWA Project                    | <https://github.com/digininja/DVWA>                              |
| OWASP Testing Guide             | <https://owasp.org/www-project-web-security-testing-guide/>      |

---

**⭐ If this project was useful or interesting, please star the repository**

