# 🔐 Secure Branch Office Network Design (VLAN + ACL)

### Joseph Abidoye

[![Type](https://img.shields.io/badge/Type-Network%20Security-blue?style=for-the-badge)]()
[![Target](https://img.shields.io/badge/Target-Simulated%20Branch%20Office-orange?style=for-the-badge)]()
[![Tools](https://img.shields.io/badge/Tools-Cisco%20Packet%20Tracer-blue?style=for-the-badge)]()
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

This project designs a segmented branch-office network that isolates departments (Admin, Sales,
IT) into separate VLANs and enforces least-privilege access between them using ACLs. The goal was
to demonstrate that network segmentation only becomes meaningful when paired with verified access
control not just VLAN separation on its own.

### What This Project Demonstrates

- VLAN design and configuration across multiple departments
- Inter-VLAN routing using router-on-a-stick with sub-interfaces
- Least-privilege ACL writing to restrict cross-department access
- Verification discipline confirming rules work via live testing, not assumption

---

## 🖥️ Environment

| Component        | Details                             |
| ------------------ | ---------------------------------------- |
| **Simulator**        | Cisco Packet Tracer                       |
| **Departments**      | Admin, Sales, IT (each on its own VLAN)   |
| **Routing Model**    | Router-on-a-stick (single physical link, sub-interfaces per VLAN) |

```
┌─────────────────────────────────────────────────────┐
│                    Branch Office LAN                │
│                                                     │
│   VLAN 10 (Admin)   VLAN 20 (Sales)   VLAN 30 (IT)  │
│        │                  │                 │       │
│        └──────────────────┼─────────────────┘       │
│                            │                        │
│                     Trunk Port (Switch)             │
│                            │                        │
│                Router-on-a-Stick (sub-interfaces)   │
└─────────────────────────────────────────────────────┘
```

---

## 🛠️ Tools Used

| Tool                  | Purpose                                    |
| ------------------------ | ------------------------------------------------ |
| **Cisco Packet Tracer**   | Network simulation and configuration              |
| **Cisco IOS**             | Switch and router configuration syntax             |

---

## 📐 Methodology / Steps

```
Phase 1: Design VLAN structure per department
         ↓
Phase 2: Configure trunk ports between switch and router
         ↓
Phase 3: Configure router-on-a-stick inter-VLAN routing
         ↓
Phase 4: Write ACLs enforcing least-privilege access
         ↓
Phase 5: Verify with live ping tests
```

### Phase 1 - VLAN Design

**Objective:** Segment the network into three department-based VLANs.

```
vlan 10
 name Admin
vlan 20
 name Sales
vlan 30
 name IT
```

**Result:** Three VLANs created, each mapped to its department's access ports.

### Phase 2 - Trunk Configuration

**Objective:** Allow all VLAN traffic to pass over a single physical link between switch and
router.

```
interface FastEthernet0/1
 switchport mode trunk
```

**Result:** Trunk link established, carrying tagged traffic for all three VLANs.

### Phase 3 - Inter-VLAN Routing

**Objective:** Enable devices on different VLANs to communicate through the router.

```
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

**Result:** Router-on-a-stick configuration active; devices on separate VLANs able to route
through the appropriate sub-interface.

### Phase 4 - ACL Enforcement

**Objective:** Deny Sales VLAN access to Admin/Payroll resources while permitting IT full access.

```
access-list 110 deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 110 permit ip any any
```

**Result:** ACL applied to the appropriate sub-interface, blocking Sales → Admin traffic while
leaving other paths open.

### Phase 5 - Verification

**Objective:** Confirm the ACL behaves as intended using live ping tests between VLANs.

**Result:** Pings from Sales to Admin blocked as expected; pings from IT to Admin succeeded,
confirming the least-privilege model was correctly enforced.

---

## 🔍 Key Findings / Results

| Metric                          | Result                                  |
| ------------------------------- | ---------------------------------------- |
| VLANs configured                 | 3 (Admin, Sales, IT)                     |
| Inter-VLAN routing model         | Router-on-a-stick                        |
| ACL enforcement verified          | Yes - Sales → Admin blocked via live ping test |
| IT access preserved               | Yes - full access confirmed              |

**Takeaway:** VLAN segmentation alone only separates broadcast domains — it took an explicit ACL,
verified with real traffic tests, to actually enforce least-privilege access between departments.

---

## 📊 Full Report

Full configuration files, topology diagram, and verification screenshots are documented in this
project's folder in the main portfolio repository. [Find Full Report Here](https://github.com/iamtimofe/Joseph-Abidoye-Cybersecurity-Portfolio/blob/main/Networking/Network-Segmentation-and-ACL.md)

---

## 📚 Lessons Learned

**1. VLANs segment traffic they don't restrict it**
Without ACLs, VLANs on the same router will happily route traffic between each other by default.
Segmentation and access control are two separate controls that both have to be configured.

**2. "It should work" is not verification**
The ACL looked correct on paper before testing live ping tests were what actually confirmed the
Sales → Admin path was blocked and the IT → Admin path wasn't.

**3. Sub-interface design scales cleanly**
Router-on-a-stick with per-VLAN sub-interfaces made adding a new department later a matter of one
new sub-interface and one new ACL line, not a full redesign.

---


## 📖 References

| Resource                     | URL                                                       |
| ------------------------------- | -------------------------------------------------------------- |
| Cisco Inter-VLAN Routing Guide   | <https://www.cisco.com/c/en/us/support/docs/lan-switching/inter-vlan-routing/> |
| Cisco Standard & Extended ACLs   | <https://www.cisco.com/c/en/us/support/docs/security/ios-access-lists/> |

---

**⭐ If this project was useful or interesting, please star the repository**

