# Phishing Investigation Report

## Case Information

**Case ID:** CASE-001

**Investigator:** Folayinka

**Investigation Date:** July 14, 2026

---

## Summary

A phishing website was identified through PhishTank.

The domain resolved successfully and was accessible at the time of investigation.

VirusTotal reported one security vendor (ESET) detecting the URL as phishing.

---

## Indicators of Compromise (IOCs)

### Domain

bbgoverno.digital

### URL

hxxps://bbgoverno[.]digital/appcx/index.html

### IP Address

5.230.71.248

### Name Servers

ns1.dyna-ns.net

ns2.dyna-ns.net

---

## DNS Findings

- IPv4 (A Record) present
- No IPv6 (AAAA) record
- No MX record
- No TXT record

---

## VirusTotal

Detection Ratio:

1 / 92

Detected By:

- ESET (Phishing)

---

## Infrastructure Findings

- Reverse DNS lookup returned NXDOMAIN.
- HTTPS certificate hostname mismatch observed.
- Website responded with HTTP 200 OK.

---


## HTTP Header Analysis

The web server responded with an HTTP 302 redirect to:

appcx/index.html

Observed HTTP response headers:

- Server: nginx
- PHP session cookie issued (PHPSESSID)
- Cookie support verification (cookie_test)
- HSTS enabled
- Cache disabled (no-store, no-cache)

These findings indicate the phishing infrastructure is actively serving a web application and redirecting visitors to the phishing landing page.


## Analyst Assessment

Based on the PhishTank listing, VirusTotal detection, active web service, and DNS analysis, the investigated domain is consistent with phishing infrastructure.

Further monitoring and blocking of the domain and associated IP address are recommended.


## IP Intelligence

**IP Address:** 5.230.71.248

**Country:** Germany

**City:** Frankfurt am Main

**Hosting Provider:** GHOSTnet GmbH

**Company:** GHOSTnet Network used for VPS Hosting Services

**ASN:** AS12586

**Hostname:** None observed

**Abuse Contact:** abuse@ghostnet.de

### Analyst Notes

The phishing infrastructure is hosted on a VPS network operated by GHOSTnet GmbH in Frankfurt, Germany. The IP belongs to a hosting provider, which does not imply the provider is malicious. The absence of a hostname is consistent with the reverse DNS lookup performed earlier.


## AbuseIPDB Intelligence

**Abuse Confidence Score:** 0%

**Total Reports:** 0

**ISP:** GHOSTnet Network used for VPS Hosting Services

**Usage Type:** Data Center / Web Hosting / Transit

**ASN:** AS12586

**Country:** Germany

### Analyst Notes

No abuse reports were present for the IP address at the time of investigation. This should not be interpreted as evidence that the infrastructure is benign. Other intelligence sources (PhishTank and VirusTotal) identified the associated domain and URL as phishing-related, indicating that the infrastructure may be newly deployed or not yet widely reported.
