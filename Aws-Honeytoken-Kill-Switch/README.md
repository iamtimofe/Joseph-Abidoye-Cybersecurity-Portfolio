# 🔐 AWS Honeytoken Detection & Automated Kill-Switch

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-Cloud%20Detection%20%26%20Response-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-AWS%20eu--north--1-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-CloudTrail%20%7C%20EventBridge%20%7C%20Lambda-blue?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Completed-green?style=for-the-badge)]()

---

> **⚠️ Note:** This project was built entirely in a personal, isolated AWS account (region
> `eu-north-1`) using a synthetic honeytoken secret created solely for this exercise. No
> production systems, real credentials, or third-party infrastructure were involved.

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

This project simulates the detection and automated containment phase of a cloud breach response
workflow. A honeytoken secret was planted in AWS Secrets Manager as bait; any access to it triggers
one of two parallel detection paths (CloudWatch metric filters or EventBridge event rules), which in
turn fires an SNS alert and a Lambda function that automatically strips IAM permissions from the
offending user closing the window between detection and containment to seconds rather than
minutes.

### What This Project Demonstrates

- Ability to design an automated cloud detection-and-response pipeline, not just a static alert
- Comparative evaluation of AWS-native detection mechanisms by real response latency
- IAM automation for incident containment (least-privilege quarantine, not account deletion)
- Full forensic evidence handling CloudTrail logs, alert emails, before/after IAM state

---

## 🖥️ Environment

| Component          | Details                                              |
| -------------------- | ------------------------------------------------------ |
| **Cloud Provider**    | AWS                                                    |
| **Region**            | `eu-north-1`                                           |
| **Bait Resource**     | AWS Secrets Manager secret (`Production_Database_Credentials`) |
| **Detection Layer**   | CloudTrail → CloudWatch Metric Filters & EventBridge Rules |
| **Response Layer**    | Lambda function with `AWSDenyAll` permissions boundary |
| **Notification**      | SNS email alert                                        |

```
┌─────────────────────────────────────────────┐
│                AWS · eu-north-1              │
│                                               │
│   Secrets Manager (honeytoken)               │
│           │ GetSecretValue                   │
│           ▼                                  │
│   CloudTrail  ──┬──► CloudWatch Metric Filter (~3–5 min)
│                 └──► EventBridge Rule (<10 sec)
│                          │                    │
│                          ▼                    │
│                     SNS Alert (email)         │
│                          │                    │
│                          ▼                    │
│           Lambda Kill-Switch (DetachUserPolicy)│
└─────────────────────────────────────────────┘
```

---

## 🛠️ Tools Used

| Tool                    | Purpose                                                  |
| ------------------------- | ----------------------------------------------------------- |
| **AWS Secrets Manager**   | Hosts the honeytoken bait secret                            |
| **AWS CloudTrail**        | Logs every API call, including unauthorized secret access   |
| **AWS CloudWatch**        | Metric filter-based detection path (polling, slower)        |
| **AWS EventBridge**       | Event-driven detection path (near-real-time)                |
| **AWS Lambda**            | Executes the automated IAM kill-switch on trigger            |
| **AWS IAM**                | Target of the automated quarantine action                    |
| **Amazon SNS**            | Sends the human-readable alert email                         |

---

## 📐 Methodology / Steps

```
Phase 1: Plant the honeytoken secret
         ↓
Phase 2: Configure CloudTrail logging
         ↓
Phase 3: Build CloudWatch metric-filter detection path
         ↓
Phase 4: Build EventBridge event-rule detection path
         ↓
Phase 5: Build Lambda kill-switch + SNS alerting
         ↓
Phase 6: Simulate unauthorized access & compare response times
```

### Phase 1 - Plant the Honeytoken

**Objective:** Create a decoy secret with no legitimate business use, so any access to it is
inherently suspicious.

```
aws secretsmanager create-secret \
  --name Production_Database_Credentials \
  --secret-string '{"username":"admin","password":"honeytoken-bait"}'
```

**Result:** Bait secret live in `eu-north-1`, indistinguishable from a real credential at a glance.

### Phase 2 - CloudTrail Logging

**Objective:** Ensure every `GetSecretValue` call against the honeytoken is captured.

**Result:** Management events logging confirmed active across the account; all API calls
timestamped and attributable to an IAM principal.

### Phase 3 - CloudWatch Detection Path

**Objective:** Build a metric filter against the CloudTrail log group that fires on any
`GetSecretValue` call for the honeytoken ARN.

**Result:** Alarm triggers reliably, but with a **3–5 minute** delay due to CloudWatch Logs
ingestion and metric evaluation periods.

### Phase 4 - EventBridge Detection Path

**Objective:** Build an EventBridge rule matching the same API call directly off the CloudTrail
event stream, bypassing the CloudWatch Logs pipeline.

**Result:** Rule triggers in **under 10 seconds** the event-driven path is roughly 20–30x faster
than the polling-based CloudWatch path.

### Phase 5 - Lambda Kill-Switch

**Objective:** On trigger, automatically strip the offending IAM user's permissions rather than
waiting for manual response.

```
# Lambda logic (simplified)
iam.detach_user_policy(UserName=offending_user, PolicyArn=AWSDenyAll_boundary_arn)
```

**Result:** Compromised IAM user quarantined to zero-permission state within seconds of the
EventBridge trigger firing, with an SNS email confirming the action.

### Phase 6 - Simulated Access & Timing Comparison

**Objective:** Access the honeytoken as an unauthorized test user and time both detection paths
end-to-end.

**Result:** EventBridge path: detection + containment complete in <10s. CloudWatch path: detection
alone took 3–5 minutes, with containment following after.

---

## 🔍 Key Findings / Results

| Metric                          | Result             |
| ---------------------------------- | -------------------- |
| EventBridge detection latency       | < 10 seconds         |
| CloudWatch metric filter latency    | 3–5 minutes           |
| Automated containment action        | IAM policy detach (working) |
| Forensic trail completeness         | Full CloudTrail JSON, SNS email, before/after IAM state captured |

**Takeaway:** Event-driven detection (EventBridge) meaningfully outperforms polling-based detection
(CloudWatch metric filters) for time-sensitive response scenarios a material difference in any
environment where dwell time matters, such as banking or fintech infrastructure.

---

## 📊 Full Report

Full write-up, screenshots, and raw CloudTrail JSON evidence are in this project's folder in the
main portfolio repository. [Find Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/Aws-Honeytoken-Kill-Switch/AWS%20Honeytoken%20Detection%20%26%20Automated%20Kill-Switch.md)

### Next Hardening Priorities

```
IMMEDIATE:
├── Standardize on EventBridge for all future honeytoken-style detections
└── Extend kill-switch to also revoke active sessions, not just detach policies

SHORT TERM:
├── Add a second honeytoken type (fake API key) to test detection breadth
└── Route SNS alerts into a Slack/Teams webhook for faster human triage

ONGOING:
└── Periodically rotate honeytoken values to avoid staleness
```

---

## 📚 Lessons Learned

**1. Event-driven beats polling for time-sensitive detection**
The 20–30x latency gap between EventBridge and CloudWatch metric filters isn't a rounding error —
it's the difference between catching an attacker mid-session and finding out after the fact.

**2. Automated response needs a floor, not just a ceiling**
Detaching IAM policies (quarantine) rather than deleting the user preserves forensic value and
avoids destroying evidence, while still neutralizing the immediate threat.

**3. Honeytokens are only as good as their believability**
A bait secret with a realistic name (`Production_Database_Credentials`) is far more likely to be
touched by a real attacker than one with an obviously fake name — naming discipline matters.

---

## 📖 References

| Resource                          | URL                                                       |
| ------------------------------------ | ------------------------------------------------------------ |
| AWS Secrets Manager Documentation     | <https://docs.aws.amazon.com/secretsmanager/>                |
| AWS EventBridge Documentation         | <https://docs.aws.amazon.com/eventbridge/>                   |
| AWS CloudTrail Documentation          | <https://docs.aws.amazon.com/cloudtrail/>                    |
| AWS Lambda Documentation              | <https://docs.aws.amazon.com/lambda/>                        |
| MITRE ATT&CK — Cloud Credential Access | <https://attack.mitre.org/tactics/TA0006/>                  |

---

**⭐ If this project was useful or interesting, please star the repository**

