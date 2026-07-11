# 🔐 Applied Cryptography & Secure Web Server Lab

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-Cryptography-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-Local%20Apache%20Server-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-OpenSSL%20%7C%20Wireshark-blue?style=for-the-badge)]()
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

This project builds hands-on intuition for symmetric and asymmetric encryption using OpenSSL, then
proves at the packet level using Wireshark exactly why HTTPS matters over plain HTTP. The goal
was to move cryptography from abstract theory to something demonstrably visible in captured
network traffic.

### What This Project Demonstrates

- Practical use of AES-256-CBC for symmetric encryption/decryption
- Practical use of RSA-2048 for asymmetric key generation and encryption
- Ability to stand up a self-signed TLS certificate on Apache
- Packet-level proof of the real-world risk of unencrypted HTTP traffic

---

## 🖥️ Environment

| Component        | Details                     |
| ------------------ | ------------------------------- |
| **Attacker/Analyst OS** | Kali Linux                  |
| **Web Server**           | Apache HTTP Server           |
| **Certificate Type**     | Self-signed TLS certificate   |

---

## 🛠️ Tools Used

| Tool          | Purpose                                             |
| --------------- | ---------------------------------------------------------- |
| **OpenSSL**       | Symmetric/asymmetric encryption, key generation, cert creation |
| **Apache**        | Web server hosting both HTTP and HTTPS endpoints             |
| **Wireshark**      | Packet capture and traffic comparison                        |

---

## 📐 Methodology / Steps

```
Phase 1: Symmetric encryption with AES-256-CBC
         ↓
Phase 2: Asymmetric encryption with RSA-2048
         ↓
Phase 3: Stand up Apache with a self-signed TLS certificate
         ↓
Phase 4: Capture and compare HTTP vs. HTTPS traffic in Wireshark
```

### Phase 1 - Symmetric Encryption (AES-256-CBC)

**Objective:** Encrypt and decrypt a file using a symmetric key.

```
openssl enc -aes-256-cbc -salt -in plaintext.txt -out encrypted.bin
openssl enc -d -aes-256-cbc -in encrypted.bin -out decrypted.txt
```

**Result:** File successfully encrypted and decrypted, confirming the correct key round-trips
cleanly.

### Phase 2 - Asymmetric Encryption (RSA-2048)

**Objective:** Generate an RSA key pair and use it for asymmetric encryption/decryption.

```
openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -pubout -in private.pem -out public.pem
```

**Result:** 2048-bit key pair generated; message encrypted with the public key and successfully
decrypted only with the corresponding private key.

### Phase 3 - Self-Signed TLS Certificate

**Objective:** Configure Apache to serve HTTPS using a self-signed certificate.

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout apache.key -out apache.crt
```

**Result:** Apache successfully serving both HTTP (port 80) and HTTPS (port 443) endpoints for
comparison.

### Phase 4 - Traffic Capture & Comparison

**Objective:** Capture and compare a login request over HTTP versus the same request over HTTPS.

**Result:** HTTP capture showed the full request including credentials in readable plaintext.
HTTPS capture showed only encrypted TLS record data, with no readable credential content.

---

## 🔍 Key Findings / Results

| Metric                              | Result                             |
| -------------------------------------- | -------------------------------------- |
| AES-256-CBC round-trip                  | Successful                             |
| RSA-2048 key pair generation             | Successful                             |
| HTTP traffic (Wireshark)                 | Credentials visible in plaintext        |
| HTTPS traffic (Wireshark)                 | Fully encrypted, no readable credentials |

**Takeaway:** Seeing plaintext credentials sitting in a Wireshark capture over HTTP made the case
for HTTPS in a way no slide deck ever could the difference between the two captures is the
entire argument for TLS in one screenshot.

---

## 📊 Full Report

Full command output, key files, and Wireshark capture screenshots are documented in this project's
folder in the main portfolio repository. [Find Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/Cryptography/Encryption-and-Traffic-Analysis.md)

---

## 📚 Lessons Learned

**1. Symmetric vs. asymmetric is a speed/trust trade-off, not just a technical distinction**
AES is fast but requires securely sharing a key; RSA solves the key-sharing problem but is far
more computationally expensive  which is exactly why TLS uses both together in practice.

**2. A self-signed certificate is enough to prove the concept, but not enough for trust**
Apache served HTTPS correctly with a self-signed cert, but browsers still flagged it as untrusted
a good reminder of why certificate authorities exist.

**3. Seeing is more convincing than being told**
Explaining "HTTP is insecure" is abstract. Watching a password appear in cleartext inside
Wireshark's Follow TCP Stream view is not.

---

## 📖 References

| Resource                  | URL                                            |
| ----------------------------- | -------------------------------------------------- |
| OpenSSL Documentation           | <https://docs.openssl.org/>                          |
| Apache SSL/TLS Configuration    | <https://httpd.apache.org/docs/2.4/ssl/>              |
| Wireshark User Guide            | <https://www.wireshark.org/docs/wsug_html/>            |

---

**⭐ If this project was useful or interesting, please star the repository**
