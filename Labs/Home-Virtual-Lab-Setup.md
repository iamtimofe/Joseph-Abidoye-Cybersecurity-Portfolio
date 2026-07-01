# 🖥️ Home Virtual Lab Setup (Kali Linux + Ubuntu)

## 🎯 Objective
To build a personal cybersecurity practice environment using virtual machines for networking and Linux security practice.

---

## 🛠️ Tools Used
- VirtualBox
- Kali Linux
- Ubuntu
- Bridged Network Adapter
- Linux Terminal

---

## 📌 Lab Setup Process

### 1️⃣ Installed VirtualBox
Downloaded and installed VirtualBox to host multiple virtual machines.

### 2️⃣ Deployed Kali Linux
- Imported Kali Linux ISO
- Allocated RAM and storage
- Installed successfully

### 3️⃣ Deployed Ubuntu
- Installed Ubuntu in a separate VM
- Configured system settings

### 4️⃣ Configured Network (Bridged Mode)
- Set both VMs to use Bridged Adapter demonstrate real network communication
- Verified IP addresses using:
 ```bash
ip a
 ```
### 5️⃣ Verified Connectivity
- Confirmed both VMs received valid IPs on the same subnet via bridged mode
- Pinged between Kali and Ubuntu VMs to confirm they could reach each other
- Pinged the host machine's gateway to confirm internet-facing connectivity

---

## 📚 What I Learned
- How bridged networking differs from NAT and why it matters for lab realism
- Basic VM resource allocation trade-offs (RAM/storage vs host performance)
- Troubleshooting steps when a VM doesn't get an IP on first boot
