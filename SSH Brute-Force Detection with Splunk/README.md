# 🔐 SSH Brute-Force Detection with Splunk

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-SIEM%20%2F%20Detection%20Engineering-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-Linux%20Auth%20Logs-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-Splunk%20%7C%20SPL-blue?style=for-the-badge)]()
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

This project detects SSH brute-force login attempts from raw Linux authentication logs using
Splunk SPL, working against a deliberately noisy, unbalanced synthetic dataset. The goal was to
isolate genuine attack patterns from routine authentication noise and map the confirmed activity
to its corresponding MITRE ATT&CK technique.

### What This Project Demonstrates

- Ability to write threshold-based SPL detection queries from scratch
- Comfort working with large, noisy log datasets (12,500+ events)
- Understanding of detection threshold tuning trade-offs (false positives vs. missed detections)
- Mapping raw log findings to a recognized threat framework (MITRE ATT&CK)

---

## 🖥️ Environment

| Component        | Details                                  |
| ------------------ | ------------------------------------------- |
| **Platform**        | Splunk Enterprise 10.4.0                    |
| **Data Source**      | Synthetic Linux `auth.log` dataset           |
| **Event Volume**     | 12,500+ authentication events                |
| **Log Type**         | SSH `failed password` / `accepted password` entries |

---

## 🛠️ Tools Used

| Tool                | Purpose                                        |
| --------------------- | ------------------------------------------------- |
| **Splunk Enterprise**  | Log ingestion, search, and visualization           |
| **SPL**                | Query language used to build all detection logic   |

---

## 📐 Methodology / Steps

```
Phase 1: Ingest & explore the raw auth log dataset
         ↓
Phase 2: Build threshold-based brute-force detection query
         ↓
Phase 3: Rank attacking source IPs independent of target account
         ↓
Phase 4: Build a timechart to isolate attack burst windows
         ↓
Phase 5: Map findings to MITRE ATT&CK
```

### Phase 1 - Ingest & Explore

**Objective:** Load the dataset and get a feel for its size and noise level before writing any
detection logic.

**Result:** 12,500+ events confirmed, heavily unbalanced mostly noise, with a smaller number of
concentrated failure bursts from a handful of source IPs.

### Phase 2 - Threshold-Based Detection

**Objective:** Isolate IP/username pairs with an abnormal number of failed login attempts.

```spl
index=auth sourcetype=linux_secure "Failed password"
| stats count by src_ip, user
| where count > 5
```

**Result:** Threshold-based query successfully isolated the brute-force IP/username pairs from the
background noise of legitimate failed logins.

### Phase 3 - Attacker Ranking

**Objective:** Rank source IPs by total failure volume, independent of which account they were
targeting, to build a blocklist candidate list.

```spl
index=auth sourcetype=linux_secure "Failed password"
| stats count by src_ip
| sort -count
```

**Result:** A small number of IPs accounted for the overwhelming majority of failed attempts —
clear blocklist candidates.

### Phase 4 - Timechart / Burst Detection

**Objective:** Visualize failure volume over time to identify the exact windows of attack activity.

```spl
index=auth sourcetype=linux_secure "Failed password"
| timechart span=5m count
```

**Result:** A 5-minute timechart pinpointed the attack burst window precisely 391 failed events
within a single 15-minute period, far above the background rate.

### Phase 5 - MITRE ATT&CK Mapping

**Objective:** Formally tie the detected activity to a named adversary technique.

**Result:** Activity mapped to **T1110.001 Brute Force: Password Guessing**.

---

## 🔍 Key Findings / Results

| Metric                              | Result                          |
| -------------------------------------- | ---------------------------------- |
| Total events analyzed                   | 12,500+                            |
| Confirmed brute-force burst volume      | 391 events / 15 minutes             |
| Detection method                        | Threshold-based SPL (`count > 5`)   |
| MITRE ATT&CK mapping                    | T1110.001 (Brute Force: Password Guessing) |

**Takeaway:** Raw log volume is not the same as signal a handful of well-chosen SPL commands
(`stats`, `where`, `timechart`) turned 12,500+ noisy events into a precise, actionable detection.

---

## 📊 Full Report

Full SPL queries, screenshots, and search results are documented in this project's folder in the
main portfolio repository. [Find Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/SSH%20Brute-Force%20Detection%20with%20Splunk/Detecting%20SSH%20brute-force%20activity%20from%20Linux%20authentication%20logs%20using%20Splunk.md)

---

## 📚 Lessons Learned

**1. Threshold tuning is a judgment call, not a formula**
Set the threshold too low and legitimate users with a mistyped password get flagged constantly;
set it too high and slow, low-and-slow brute-force attempts slip through undetected.

**2. Ranking by source, not by target, reveals the real attacker**
Grouping by `src_ip` alone (rather than by targeted username) surfaced the actual attacking hosts
much faster than looking at any single account's failure history.

**3. Time-boxing an attack matters for response, not just detection**
Knowing *that* a brute-force happened is useful; knowing the exact 15-minute window it happened in
is what makes an incident report actionable.

---



## 📖 References

| Resource                              | URL                                              |
| ---------------------------------------- | --------------------------------------------------- |
| Splunk SPL Search Reference               | <https://docs.splunk.com/Documentation/Splunk/latest/SearchReference> |
| MITRE ATT&CK — T1110.001                  | <https://attack.mitre.org/techniques/T1110/001/>     |

---

**⭐ If this project was useful or interesting, please star the repository**

*Part of an ongoing cybersecurity portfolio [github.com/iamtimofe](https://github.com/iamtimofe)*
