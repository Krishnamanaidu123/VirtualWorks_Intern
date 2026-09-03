# Virtual Lab Setup

## Task 2: Kali Linux Virtual Machine Installation

![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white) ![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge) ![VMware](https://img.shields.io/badge/VMware-607078?style=for-the-badge&logo=vmware&logoColor=white)

---

## 📖 Overview

This document outlines the complete process of setting up a secure, isolated, and fully functional cybersecurity virtual lab. The lab is built around **Kali Linux**, the industry-standard operating system for penetration testing and security auditing, running on a hypervisor (VirtualBox or VMware).

**Objective:** To establish a safe, controlled environment that allows for hands-on practice with ethical hacking tools, vulnerability assessment, and network analysis without risking damage to the host machine or production networks.

**Task ID:** `task2`

---

## 🗂️ Table of Contents

1. [What is a Virtual Lab?](#-what-is-a-virtual-lab)
2. [Why Kali Linux?](#-why-kali-linux)
3. [Hardware & Software Prerequisites](#-hardware--software-prerequisites)
4. [Network Modes Explained](#-network-modes-explained-critical)
5. [Step-by-Step Installation Guide](#-step-by-step-installation-guide)
6. [Post-Installation Setup & Customization](#-post-installation-setup--customization)
7. [Lab Architecture](#-lab-architecture)
8. [Safety, Ethics, & Target Practice](#-safety-ethics--target-practice)
9. [Proof of Completion](#-proof-of-completion)
10. [Troubleshooting Common Issues](#-troubleshooting-common-issues)

---

## 🖥️ What is a Virtual Lab?

A **virtual lab** is a sandboxed environment created using virtualization software. It mimics physical hardware components (CPU, RAM, storage, network adapters) to run multiple operating systems simultaneously on a single physical machine.

**Why Virtualization Matters in Cybersecurity:**

| Benefit | Description |
| :--- | :--- |
| **Isolation** | Malware or broken configurations are contained within the VM and cannot affect the host OS. |
| **Snapshots** | You can save the exact state of the VM and revert to it instantly if something goes wrong. |
| **Cost-Effectiveness** | Run multiple machines (e.g., Kali, Windows, Metasploitable) on one laptop. |
| **Reproducibility** | Easily spin up identical environments for training or certification labs. |

---

## 🐉 Why Kali Linux?

Kali Linux is a Debian-based distribution specifically built for **advanced penetration testing** and **security auditing**. It comes pre-installed with hundreds of tools tailored for various information security tasks.

### Key Tools Included

| Category | Example Tools | Purpose |
| :--- | :--- | :--- |
| **Information Gathering** | `Nmap`, `Recon-ng`, `Maltego` | Network scanning, OS fingerprinting, and OSINT. |
| **Vulnerability Assessment** | `OpenVAS`, `Nikto`, `Burp Suite` | Web application scanning and vulnerability identification. |
| **Exploitation** | `Metasploit Framework`, `SearchSploit` | Developing and executing exploits against vulnerable targets. |
| **Password Attacks** | `John the Ripper`, `Hashcat`, `Hydra` | Brute-forcing and cracking passwords. |
| **Sniffing & Spoofing** | `Wireshark`, `Bettercap`, `Ettercap` | Capturing and analyzing network traffic. |
| **Post-Exploitation** | `Empire`, `PowerSploit` | Maintaining access and pivoting within networks. |

---

## 🔧 Hardware & Software Prerequisites

Before beginning, ensure you have the following:

### Host System Requirements (Minimum)
- **CPU:** 64-bit processor with **Intel VT-x** or **AMD-V** virtualization extensions (enable in BIOS).
- **RAM:** 8 GB (4 GB for the host + 4 GB for Kali).
- **Storage:** 60 GB of free disk space.
- **OS:** Windows, macOS, or Linux.

### Software Required
| Software | Type | Download Link |
| :--- | :--- | :--- |
| **VirtualBox** | Open-source hypervisor | [virtualbox.org](https://www.virtualbox.org/) |
| *or* **VMware Workstation Player** | Free for personal use | [vmware.com](https://www.vmware.com/products/workstation-player.html) |
| **Kali Linux ISO** | OS installation image | [kali.org/get-kali](https://www.kali.org/get-kali/) |
| *or* **Kali Pre-built VM** | OVA file for instant setup | [kali.org/get-kali](https://www.kali.org/get-kali/) |

---

## 🌐 Network Modes Explained (Critical)

Choosing the correct network mode is vital for your lab setup. Here is a breakdown:

| Mode | How It Works | Use Case |
| :--- | :--- | :--- |
| **NAT** | VM shares the host's IP address; gets internet access but is hidden from the physical network. | General browsing, updates, and isolated testing where you don't need to interact with other devices. |
| **Bridged** | VM gets its own IP on the same network as the host. | Your VM appears as a separate physical device on the network. Useful for active scanning. |
| **Host-Only** | VM can only communicate with the host and other VMs. **No internet.** | Completely isolated internal labs for CTF practice (e.g., connecting Kali to Metasploitable without external exposure). |
| **NAT Network** | Multiple VMs can talk to each other and share internet via NAT. | Ideal for multi-machine labs (e.g., Kali + Windows target). |

> **Recommendation:** Start with **NAT** for installation, then add a **Host-Only** or **NAT Network** adapter for lab practice.

---

## 🚀 Step-by-Step Installation Guide

### Phase 1: Enable Virtualization in BIOS
1. Restart your computer.
2. Enter BIOS/UEFI settings (usually `F2`, `Del`, or `Esc` during boot).
3. Locate **CPU Configuration** or **Advanced** settings.
4. Enable **Intel VT-x** or **AMD SVM**.
5. Save and Exit.

### Phase 2: Create the Virtual Machine

1. Open VirtualBox/VMware and click **"New"**.
2. Enter Name: `Kali-Lab`.
3. Set Type to **Linux** and Version to **Debian (64-bit)**.
4. Allocate resources:

| Resource | Recommended Setting |
| :--- | :--- |
| **RAM** | 4096 MB (4 GB) – 8192 MB for heavy tools. |
| **CPU Cores** | 2 processors. |
| **Storage** | 40 GB (dynamically allocated preferred). |

### Phase 3: Install Kali Linux

1. Attach the downloaded Kali `.iso` file to the VM's optical drive.
2. Start the VM.
3. Select **"Graphical Install"**.
4. Follow the prompts:
    - **Language/Location:** Choose your preferences.
    - **Network Mirror:** Uncheck (unless you want to use a local mirror) – you can update later.
    - **Partitioning:** Select **"Guided – use entire disk"** (inside the VM).
    - **Software Selection:** Leave defaults (Xfce or GNOME is fine).
    - **GRUB:** Install the boot loader to `/dev/sda` (the virtual disk).
5. Reboot the VM.

---

## 🛠️ Post-Installation Setup & Customization

Once the VM boots, perform the following essential steps:

### 1. Update the System
Open a terminal and run:

```bash
sudo apt update && sudo apt full-upgrade -y
```

### 2. Install VirtualBox Guest Additions (if using VirtualBox)
This enables seamless mouse integration and screen resizing.

```bash
sudo apt install -y virtualbox-guest-x11
sudo reboot
```

### 3. Install VMware Tools (if using VMware)

```bash
sudo apt install -y open-vm-tools-desktop
sudo reboot
```

### 4. Set a Static IP (Optional for Host-Only)
If you plan to use a host-only network, configure it manually:

```bash
sudo nano /etc/network/interfaces
```

Add the following:

```text
auto eth1
iface eth1 inet static
    address 192.168.56.101
    netmask 255.255.255.0
    gateway 192.168.56.1
```

Restart networking:

```bash
sudo systemctl restart networking
```

### 5. Change the Default Password (Highly Recommended)

```bash
sudo passwd root
```

### 6. Install Additional Tools (if missing)

```bash
sudo apt install -y exploitdb bloodhound crackmapexec
```

---

## 🏗️ Lab Architecture

Here is a visual representation of a typical multi-machine lab setup:

```text
+---------------------------------------------------+
|                  Host Computer                    |
|  (Windows/Linux/macOS - 16GB RAM recommended)     |
|                                                   |
|  +--------------------------------------------+   |
|  |         VirtualBox / VMware Hypervisor     |   |
|  |                                            |   |
|  |  +------------+  +------------+            |   |
|  |  |  Kali Linux |  | Metasploit |           |   |
|  |  |  (Attacker) |  |  able 2    |           |   |
|  |  |  IP: .101   |  | (Target)   |           |   |
|  |  |  Tools:     |  | IP: .102   |           |   |
|  |  | Nmap, MSF   |  | Vulnerable |           |   |
|  |  +------+-----+  +-----+------+            |   |
|  |         |           |                      |   |
|  |         +-----+-----+                      |   |
|  |             | (Host-Only Network)          |   |
|  +-------------+------------------------------+   |
|                |                                  |
|         (NAT/Bridged for Internet)                |
+---------------------------------------------------+
```

---

## ⚖️ Safety, Ethics & Target Practice

### Golden Rule
> **Never** run attacks against systems you do not own or do not have explicit written permission to test.

### Safe Practice Targets
To hone your skills, set up the following intentionally vulnerable environments:

| Target | Description | Download |
| :--- | :--- | :--- |
| **Metasploitable 2** | A deliberately insecure Ubuntu VM with multiple services. | [SourceForge](https://sourceforge.net/projects/metasploitable/) |
| **Metasploitable 3** | A Windows Server 2008 VM with modern vulnerabilities. | [GitHub](https://github.com/rapid7/metasploitable3) |
| **OWASP Juice Shop** | A modern web application with JavaScript/Node.js vulnerabilities. | [GitHub](https://github.com/juice-shop/juice-shop) |
| **DVWA** | Damn Vulnerable Web Application (PHP/MySQL). | [GitHub](https://github.com/digininja/DVWA) |
| **HackTheBox / TryHackMe** | Online platforms with legal CTF machines (VPN required). | [hackthebox.com](https://www.hackthebox.com/) |

### Creating Snapshots (Safety Net)
Before any complex experiment, take a snapshot:
1. In VirtualBox: `Machine > Take Snapshot`.
2. In VMware: `VM > Snapshot > Take Snapshot`.

This allows you to revert if you break the OS or want a clean state.

---

## 📸 Proof of Completion

To verify the successful setup for your internship portal, provide the following screenshots:

1. **Virtual Machine Settings**
   - Show the VM configuration (RAM, CPU, Storage) in VirtualBox/VMware.

2. **Kali Linux Desktop**
   - A full screenshot of the Kali Linux desktop environment after boot.

3. **System Verification (Terminal)**
   - Run the following commands and take a screenshot of the output:

   ```bash
   uname -a
   ```

   *Expected output:* Kernel version and architecture.

   ```bash
   ip addr
   ```

   *Expected output:* Network interfaces and assigned IP addresses.

4. **Tool Verification (Optional)**
   - Show that key tools are available:

   ```bash
   nmap --version
   wireshark --version
   msfconsole --version
   ```

---

## 🐞 Troubleshooting Common Issues

| Issue | Cause | Solution |
| :--- | :--- | :--- |
| **"VT-x is disabled"** | BIOS virtualization is off. | Enable **Intel VT-x** / **AMD SVM** in BIOS. |
| **Kali runs extremely slow** | Insufficient RAM or CPU cores. | Allocate at least 4 GB RAM and 2 CPU cores. |
| **No network/internet** | Wrong network adapter mode or missing drivers. | Switch to **NAT** or **Bridged**. Restart networking: `sudo systemctl restart NetworkManager`. |
| **Screen resolution stuck at 800x600** | Guest Additions not installed. | Install `virtualbox-guest-x11` or `open-vm-tools-desktop`. |
| **"Failed to start" after upgrade** | Kernel panic or broken dependencies. | Boot from an older kernel in GRUB or restore from a snapshot. |
| **Cannot find Metasploit** | Not installed by default in newer builds. | Install via `sudo apt install metasploit-framework`. |

---

## ✅ Conclusion

I have successfully deployed a fully functional, isolated cybersecurity virtual lab using Kali Linux and virtualization technology. 
This environment provides a safe space to explore ethical hacking methodologies, run vulnerability assessments, and practice penetration testing. 
By mastering these fundamental lab skills, I have established a solid foundation for advanced security research and analysis.

---

> *"The best way to predict the future is to create it." — Alan Kay*
