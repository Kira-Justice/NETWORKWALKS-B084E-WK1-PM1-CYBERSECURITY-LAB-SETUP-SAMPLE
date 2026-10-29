# 🔐 Cybersecurity Lab Environment Setup
Building an isolated virtual lab for penetration testing and ethical hacking practice.

## 📌 Project Overview
This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using **Oracle VirtualBox** and **Kali Linux**. The purpose of the lab is to create a controlled, isolated environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly[cite: 1].

The lab is configured on a private virtual network (`NAT Network`) so that additional target machines (such as Windows and vulnerable VMs) can be added later for authorized security testing.

---

## 🎯 Objectives
* Install and configure Oracle VirtualBox.
* Import and set up Kali Linux as the primary attacking virtual machine.
* Create a dedicated private NAT Network (`10.0.0.0/24`) for the cybersecurity lab.
* Configure consistent static IP addressing for Kali Linux (`10.0.0.2/24`).
* Enable shared folders and clipboard drag/drop integration[cite: 1].
* Verify network connectivity, DNS resolution, and core utilities (like `nmap`).
* Create a clean baseline VM snapshot for recovery.

---

## ⚙️ Lab Configuration Summary

| Component | Configuration Details |
| :--- | :--- |
| **Host OS** | Windows 10/11. |
| **Hypervisor** | Oracle VirtualBox 7.x |
| **Security OS** | Kali Linux 2026.2 |
| **RAM Allocated** | 2048 MB|
| **Network Type** | NAT Network (`NatNetwork`) |
| **Subnet Range** | `10.0.0.0/24` |
| **Kali Static IP** | `10.0.0.2/24`|
| **Default Gateway** | `10.0.0.1`|
| **DNS Server** | `8.8.8.8`[ |
| **Future VM Range** | `10.0.0.3 – 10.0.0.99`|

---

## 🪜 Lab Setup Procedure

1. **Hypervisor & Tool Setup:** Installed **7-Zip** for archive extraction and **VirtualBox** as the hypervisor.
2. **NAT Network Creation:** Configured a custom `NatNetwork` in VirtualBox with IPv4 Prefix `10.0.0.0/24` and DHCP enabled.
3. **VM Import & Settings:** Downloaded and imported the official Kali Linux VirtualBox template[cite: 1, 3]. Configured Adapter 1 to attach to `NatNetwork` using the *Intel PRO/1000 MT Desktop* adapter type with *Allow All* promiscuous mode.
4. **Static IP Configuration:** Assigned a static IPv4 address (`10.0.0.2/24`), gateway (`10.0.0.1`), and DNS (`8.8.8.8`) via NetworkManager.
5. **Snapshot Baseline:** Took a clean VM snapshot named `Clean Kali - Network Setup` to establish a safe recovery point.

---

## 🔎 Lab Verification

| Test | Command | Expected Result |
| :--- | :--- | :--- |
| 🌐 **Check IP address** | `ip a` | Correct Kali IP displayed. |
| 📡 **Test gateway** | `ping 10.0.0.1` | Successful replies.|
| 🌍 **Test Internet** | `ping 8.8.8.8` | Successful replies|
| 🔎 **Test DNS** | `nslookup networkwalks.com` | Domain resolves |
| 🧰 **Verify Nmap** | `nmap --version` | Nmap version displayed |
| 🔄 **Verify snapshot** | Restore snapshot & run `ip a` | Baseline configuration restored|

---

## 🐞 Troubleshooting & Solutions

* **Issue: No Internet Connectivity After Static IP Configuration (VirtualBox v7 / Kali 2026)**
  * **Solution:** Fix NetworkManager DAD (Duplicate Address Detection) timeout issues by running:
    ```bash
    sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
    sudo nmcli connection down "Wired connection 1"
    sudo nmcli connection up "Wired connection 1"
    ```
* **Issue: Virtualization Error / VM Fails to Start**
  * **Solution:** Enabled hardware virtualization (**Intel VT-x** / AMD-V) in the host system's BIOS/UEFI firmware settings[.

---

## 💡 What I Learned
1. **NAT vs NAT Network:** Understanding how a NAT Network allows multiple isolated virtual machines to communicate with each other while maintaining external internet access.
2. **Static Addressing:** Configuring robust IPv4 parameters, subnet masks, gateways, and DNS resolvers in Linux.
3. **Disaster Recovery:** Utilizing VirtualBox snapshots to establish reliable restore points before executing experimental tasks.

---

## 🔐 Ethical Disclaimer
*This laboratory is intended strictly for educational purposes, self-hosted practice, and authorized security testing. Do not use these tools or techniques against unauthorized systems.*

---

## 👤 Author
* **Rahmat Ali**  
* Program: Cybersecurity at Networkwalks | Week 01 | Project: Lab Setup
