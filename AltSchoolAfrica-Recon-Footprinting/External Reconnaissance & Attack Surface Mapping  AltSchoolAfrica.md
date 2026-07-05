# External Reconnaissance & Attack Surface Mapping — AltSchoolAfrica

**Category:** Offensive Security | OSINT & Reconnaissance
**Platform:** Kali Linux VM
**Target:** altschoolafrica.com (authorized lab domain, course-sanctioned assessment)
**Status:** Complete — passive OSINT, active scanning, and attack surface prioritization

---

## Assessment Ticket

| Field | Detail |
|---|---|
| Objective | Simulate the reconnaissance phase of a security assessment against a real-world domain |
| Scope | Passive OSINT, active Nmap scanning, attack surface mapping, risk prioritization |
| Authorization | Conducted under course-sanctioned educational assessment against a designated lab domain |
| Sensitivity of Findings | All findings publicly discoverable (PUBLIC classification) |

---

## Objective

Perform the reconnaissance and footprinting phase of a security assessment against a live domain — gathering everything an attacker could learn *before* touching the target directly, then escalating to active scanning, and finally converting raw findings into a prioritized attack surface.

## Part A — Passive OSINT

| Tool | Purpose | Command |
|---|---|---|
| Amass | Subdomain enumeration | `amass enum -d altschoolafrica.com -o amass_output.txt` |
| Recon-ng | Subdomain enumeration via HackerTarget module | `modules load recon/domains-hosts/hackertarget` → `options set SOURCE altschoolafrica.com` → `run` |
| WHOIS | Domain registration intelligence | `whois altschoolafrica.com` |
| dig | DNS record enumeration (A, MX, TXT, CNAME) | `dig altschoolafrica.com A/MX/TXT/CNAME` |
| theHarvester | Email and host recovery | `theHarvester -d altschoolafrica.com -b all` |
| Google Dorking | Locating exposed public resources | `site:altschoolafrica.com filetype:pdf` |

### Evidence

- Amass scan — command and output: [`screenshots/Amass01.png`](screenshots/Amass01.png)
- Amass scan — command and output: [`screenshots/Amass02.png`](screenshots/Amass02.png)
- Amass raw output file: [`outputs/amass_output.txt`](outputs/amass_output.txt)
- Recon-ng scan — command and output: [`screenshots/recon-ng-scan.png`](screenshots/recon-ng-scan.png)
- WHOIS scan output: [`screenshots/whois-scan.png`](screenshots/whois-scan.png)
- dig commands (A/MX/TXT/CNAME) output: [`screenshots/dig-records.png`](screenshots/dig-records.png)
- theHarvester raw output file: [`outputs/theharvester_output.txt`](outputs/theharvester_output.txt)
- Google Dorking results: [`screenshots/google-dorking.png`](screenshots/google-dorking.png)

### Key Findings

| # | Finding | Source | Confidence | Sensitivity |
|---|---|---|---|---|
| 1 | Domain registration details — GoDaddy.com LLC, registered 2021-10-11, Cloudflare nameservers | WHOIS | High | Public |
| 2 | A records resolving to Cloudflare-fronted IPs | dig A | High | Public |
| 3 | MX records — Google mail servers | dig MX | High | Public |
| 4 | TXT records — Google site verification, Zoho verification, SPF policy | dig TXT | High | Public |
| 5 | CNAME records showing Cloudflare authoritative nameservers | dig CNAME | Medium | Public |
| 6 | Subdomains, IPs, ASNs and URLs (incl. a backend payment subdomain) | theHarvester | High | Public |
| 7 | Additional subdomains (students, blog) | Recon-ng | High | Public |
| 8 | Additional subdomains (actors, engineering) | Amass | High | Public |

## Part B — Active Scanning (Nmap)

| Scan | Command | Purpose |
|---|---|---|
| Host discovery | `nmap -sn altschoolafrica.com` | Confirm host is alive without a full port scan |
| Full port + version scan | `nmap -sC -sV -p- altschoolafrica.com -oA nmap_full` | Identify all open ports and running service versions |
| Aggressive scan | `nmap -A altschoolafrica.com` | OS/version detection, script scanning, traceroute |

### Evidence

- Host discovery scan: [`screenshots/nmap-host-discovery.png`](screenshots/nmap-host-discovery.png)
- Full port/version scan: [`screenshots/nmap-full-scan.png`](screenshots/nmap-full-scan.png)
- Full port scan raw output: [`outputs/nmap_scans.txt`](outputs/nmap_scans.txt)
- Aggressive scan: [`screenshots/nmap-aggressive-scan.png`](screenshots/nmap-aggressive-scan.png)
- Aggressive scan raw output: [`outputs/nmap_aggressive.txt`](outputs/nmap_aggressive.txt)

### Discovered Services (summary)

All open ports on the resolved IP (`104.21.37.155`) fronted by **Cloudflare's HTTP/HTTPS proxy** — including standard 80/443 and Cloudflare's alternate ports (2052/2053/2082/2083/2086/2087/2095/2096/8080/8443/8880). SSL certificates observed with `CN=altschoolafrica.com`.

## Part C — Attack Surface Mapping & Prioritization

Built a Data Flow Diagram (DFD) mapping external actors (users, third-party merchants) through entry points (API gateway, web app, SSH, mail server) → Cloudflare CDN/proxy → backend microservices/datastores (learning platform, user database, course data, payment services).

- Attack Surface DFD (image): [`diagrams/attack-surface-dfd.png`](diagrams/attack-surface-dfd.png)
- Attack Surface DFD (editable source): [`diagrams/attack-surface-dfd.drawio`](diagrams/attack-surface-dfd.drawio)

### Target Prioritization

| Priority | Target | Risk Statement |
|---|---|---|
| 1 | Public API Gateway (Port 443) | Exposed endpoint identified via Nmap + OSINT; APIs commonly leak data via unsecured routes or expired tokens — high risk of unauthorized access/exfiltration |
| 2 | Legacy Web Server (Port 8080) | Outdated Apache with known CVEs; unpatched legacy infrastructure raises exploitation risk |
| 3 | SSH Service (Port 22) | Open with default banner enabled; disabling banner disclosure + rate-limiting reduces brute-force/credential-stuffing risk |
| 4 | Mail Server (Google MX) | Exposed MX records; SPF/DKIM alignment needed to prevent domain spoofing and phishing |
| 5 | Payment Service Subdomain (`backend-payment.prod`) | Handles financial transactions; TLS misconfiguration flagged — high-value target for data theft or MitM |

## Tools Used

`Amass` `Recon-ng` `WHOIS` `dig` `theHarvester` `Google Dorking` `Nmap` `draw.io`

## Reflection

This project reinforced that effective reconnaissance is less about memorizing commands and more about problem-solving when tools don't cooperate. Amass v5.51.1 initially returned no results due to API licensing requirements — downgrading to v3.20.0 resolved it. theHarvester required sourcing API keys before several of its sources would work. Scanning a Cloudflare-fronted target also meant the real origin infrastructure stayed masked behind the proxy, which is itself a useful finding about the target's defensive posture. Working through these obstacles built practical fluency with OSINT tooling (Amass, WHOIS, dig, theHarvester), active enumeration with Nmap, and translating raw findings into a prioritized, risk-ranked attack surface — the foundation any security assessment is built on.

## Skills Demonstrated

`OSINT` `Subdomain Enumeration` `DNS Reconnaissance` `Nmap Service/Version Scanning` `Attack Surface Mapping (DFD)` `Risk Prioritization` `Cloudflare-Fronted Target Analysis`

---

