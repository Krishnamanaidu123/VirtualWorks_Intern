# Networking & Reconnaissance

## Task 3: Fundamentals of Network Scanning & Information Gathering

![Networking](https://img.shields.io/badge/Networking-Fundamentals-blue?style=for-the-badge&logo=cisco) ![Recon](https://img.shields.io/badge/Reconnaissance-Passive_&_Active-orange?style=for-the-badge&logo=security) ![Nmap](https://img.shields.io/badge/Nmap-Scanning-red?style=for-the-badge&logo=linux) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📖 Overview

This task covers the essential networking knowledge and reconnaissance techniques required for any cybersecurity professional. Understanding how data travels across networks, how systems are identified, and how to safely gather information about targets is the first step in vulnerability assessment and penetration testing.

**Objective:** To master fundamental networking concepts (IP addresses, DNS, ports, protocols) and perform authorized reconnaissance using industry-standard tools to collect publicly available and technical information about a target.

**Task ID:** `task3`

---

## 🗂️ Table of Contents

1. [Networking Fundamentals](#-networking-fundamentals)
   - [IP Addresses](#ip-addresses)
   - [The OSI & TCP/IP Models](#the-osi--tcpip-models)
   - [DNS Deep Dive](#dns-deep-dive)
   - [Ports & Protocols](#ports--protocols)
2. [Understanding Reconnaissance](#-understanding-reconnaissance)
   - [Passive vs. Active Reconnaissance](#passive-vs-active-reconnaissance)
   - [OSINT (Open Source Intelligence)](#osint-open-source-intelligence)
3. [Essential Kali Linux Reconnaissance Tools](#-essential-kali-linux-reconnaissance-tools)
   - [Network Configuration](#network-configuration)
   - [DNS Enumeration](#dns-enumeration)
   - [WHOIS & Domain Information](#whois--domain-information)
   - [Connectivity & Path Tracing](#connectivity--path-tracing)
4. [Advanced Port Scanning with Nmap](#-advanced-port-scanning-with-nmap)
   - [Scan Types Explained](#scan-types-explained)
   - [Service & Version Detection](#service--version-detection)
   - [OS Fingerprinting](#os-fingerprinting)
   - [Scripting Engine (NSE)](#scripting-engine-nse)
5. [Reconnaissance Workflow](#-reconnaissance-workflow)
6. [Sample Reconnaissance Report](#-sample-reconnaissance-report)
7. [Ethical & Legal Considerations](#-ethical--legal-considerations)
8. [Proof of Completion](#-proof-of-completion)
9. [Troubleshooting & Common Errors](#-troubleshooting--common-errors)

---

## 🌐 Networking Fundamentals

### IP Addresses
An **Internet Protocol (IP) address** is a unique numerical label assigned to each device participating in a computer network that uses the Internet Protocol for communication.

| Type | Format | Example | Purpose |
| :--- | :--- | :--- | :--- |
| **IPv4** | 32-bit (4 octets) | `192.168.1.10` | The most common format, running out of addresses. |
| **IPv6** | 128-bit (hexadecimal) | `2001:0db8:85a3::8a2e:0370:7334` | Designed to replace IPv4 with a vastly larger address pool. |

**Special Addresses:**
- **Loopback:** `127.0.0.1` (localhost) – refers to the device itself.
- **Private (RFC 1918):** `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` – not routable on the public internet.
- **Public:** Routable on the internet.

### The OSI & TCP/IP Models
While the OSI model has 7 layers, the practical TCP/IP model condenses this into 4 layers that directly map to how the internet works.

| TCP/IP Layer | OSI Equivalent | Protocols/Examples |
| :--- | :--- | :--- |
| **Application** | Application, Presentation, Session | HTTP, HTTPS, FTP, SSH, DNS, SMTP |
| **Transport** | Transport | TCP, UDP |
| **Internet** | Network | IPv4, IPv6, ICMP, ARP |
| **Network Access** | Data Link, Physical | Ethernet, Wi-Fi, MAC addresses |

---

## 🧩 DNS Deep Dive

The **Domain Name System (DNS)** is the "phonebook of the internet." It resolves human-readable domain names into machine-readable IP addresses.

### Common DNS Record Types

| Record | Description | Example |
| :--- | :--- | :--- |
| **A** | Maps a domain to an IPv4 address. | `google.com → 142.250.185.78` |
| **AAAA** | Maps a domain to an IPv6 address. | `google.com → 2a00:1450:4001:831::200e` |
| **CNAME** | Canonical Name – aliases one domain to another. | `www.example.com → example.com` |
| **MX** | Mail Exchange – specifies mail servers for the domain. | `example.com → mail.example.com (priority 10)` |
| **TXT** | Holds arbitrary text (often used for SPF/DKIM for email security). | `v=spf1 include:_spf.google.com ~all` |
| **NS** | Name Server – specifies the authoritative DNS servers. | `ns1.example.com` |
| **SOA** | Start of Authority – contains administrative info about the zone. | Serial number, refresh timers. |

---

## 🔌 Ports & Protocols

Ports are logical endpoints that distinguish different services running on the same IP address. They range from 0 to 65535.

### Well-Known Ports (0–1023)

| Port | Protocol | Service | Purpose |
| ---: | :--- | :--- | :--- |
| 20/21 | TCP | FTP | File Transfer Protocol (data/control). |
| **22** | TCP | **SSH** | Secure Shell – remote administration. |
| 23 | TCP | Telnet | Unencrypted remote admin (deprecated). |
| 25 | TCP | SMTP | Email transmission. |
| **53** | TCP/UDP | **DNS** | Domain name resolution. |
| **80** | TCP | **HTTP** | Unencrypted web traffic. |
| 110 | TCP | POP3 | Email retrieval. |
| 123 | UDP | NTP | Network Time Protocol. |
| 143 | TCP | IMAP | Email retrieval (more advanced). |
| **443** | TCP | **HTTPS** | Encrypted web traffic (SSL/TLS). |
| 3389 | TCP | RDP | Remote Desktop Protocol (Windows). |

### TCP vs. UDP

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection** | Connection-oriented (3-way handshake). | Connectionless (fire and forget). |
| **Reliability** | Guarantees delivery (retransmission). | No guarantee (best effort). |
| **Ordering** | Ensures packets arrive in sequence. | No ordering. |
| **Use Cases** | Web browsing, email, file transfer, SSH. | Streaming, DNS queries, VoIP, online gaming. |

---

## 🕵️ Understanding Reconnaissance

Reconnaissance (Recon) is the information-gathering phase. It is the foundation of any security assessment.

### Passive vs. Active Reconnaissance

| Type | Definition | Examples | Legality |
| :--- | :--- | :--- | :--- |
| **Passive** | Gathering information without directly interacting with the target's systems. | Google dorking, social media searches, WHOIS, DNS lookups, Shodan searches. | Generally legal (public info). |
| **Active** | Directly interacting with the target's infrastructure (sending packets). | Port scanning (Nmap), ping sweeps, vulnerability scans. | Requires explicit authorization. |

### OSINT (Open Source Intelligence)
OSINT involves collecting data from publicly available sources. Useful places include:
- Search engines (Google Dorks).
- Social media platforms (LinkedIn, Twitter).
- Public databases (WHOIS, crt.sh for SSL certificates).
- Code repositories (GitHub – accidental API keys).
- Wayback Machine (historical website data).

---

## 🛠️ Essential Kali Linux Reconnaissance Tools

### Network Configuration
Check your own machine's interfaces and routing.

```bash
# Show IP addresses and interfaces
ip addr

# Show routing table
ip route

# Alternative (legacy)
ifconfig
```

### DNS Enumeration

**`nslookup`** – Query DNS records.
```bash
# Default A record lookup
nslookup example.com

# Query specific record type
nslookup -type=MX example.com
nslookup -type=TXT example.com
```

**`dig`** – More detailed DNS querying (DNS Information Groper).
```bash
# Standard A record
dig example.com

# Specific record + short output
dig example.com MX +short

# Reverse DNS (IP to domain)
dig -x 8.8.8.8
```

**`dnsrecon`** – Automated DNS enumeration.
```bash
dnsrecon -d example.com
```

### WHOIS & Domain Information
WHOIS databases provide ownership and registration details for domains.

```bash
whois example.com
```
*Note: Many domains have privacy protection, showing proxy info instead of the actual owner.*

### Connectivity & Path Tracing

**`ping`** – Checks host availability using ICMP.
```bash
ping -c 4 example.com
```

**`traceroute`** – Maps the route packets take to reach a destination (useful for network topology).
```bash
traceroute example.com
```

**`hping3`** – Advanced packet crafting (can send custom TCP/UDP/ICMP packets).
```bash
# SYN scan to port 80
hping3 -S -p 80 example.com
```

---

## 🚀 Advanced Port Scanning with Nmap

[Nmap](https://nmap.org/) (Network Mapper) is the gold standard for network discovery and security auditing.

### Scan Types Explained

| Command | Type | Description |
| :--- | :--- | :--- |
| `-sS` | **SYN Scan** (Half-open) | Sends SYN packet; if SYN-ACK received, port is open. Does not complete handshake. Fast and stealthy. |
| `-sT` | **TCP Connect** | Completes the full TCP 3-way handshake. More accurate but easier to detect. |
| `-sU` | **UDP Scan** | Sends UDP packets. Slower and less reliable, but essential for finding UDP services (DNS, SNMP). |
| `-sA` | **ACK Scan** | Used to map firewall rules (filtered vs. unfiltered). |
| `-sN` / `-sF` / `-sX` | **Null/Fin/Xmas** | Evasion techniques using TCP flags to bypass basic firewalls. |

### Service & Version Detection
Detect not just the port, but the application and its version.

```bash
nmap -sV -sS -p- 192.168.56.101
```
- `-sV`: Version detection.
- `-p-`: Scan all 65535 ports (takes time!).

### OS Fingerprinting
Identify the operating system of the target.

```bash
nmap -O --osscan-guess 192.168.56.101
```

### Nmap Scripting Engine (NSE)
Nmap comes with powerful Lua scripts for vulnerability detection, brute forcing, and enumeration.

```bash
# List all scripts
ls /usr/share/nmap/scripts/

# Run a default set of scripts
nmap -sC 192.168.56.101

# Run a specific script (e.g., HTTP headers)
nmap --script=http-headers 192.168.56.101

# Run vulnerability detection scripts
nmap --script=vuln 192.168.56.101
```

### Advanced Nmap Example

```bash
# Aggressive scan: OS detection, version detection, script scanning, and traceroute
nmap -A -T4 -p 1-1000 192.168.56.101
```
- `-A`: Aggressive mode (enables OS, version, scripts, and traceroute).
- `-T4`: Timing template (faster, more aggressive timing).

---

## 📊 Reconnaissance Workflow

A structured approach ensures no information is missed.

```mermaid
graph TD
    A[Start: Target Domain/IP] --> B[Passive Recon]
    B --> C[WHOIS Lookup]
    B --> D[DNS Enumeration nslookup/dig/dnsrecon]
    B --> E[Google Dorking / OSINT]
    C --> F[Active Recon (Authorized)]
    D --> F
    E --> F
    F --> G[Ping Sweep / Live Host Discovery]
    G --> H[Port Scanning nmap -sS -sV]
    H --> I[Service & Version Detection]
    I --> J[NSE Scripts / Vulnerability Checks]
    J --> K[Document Findings]
    K --> L[Ready for Exploitation Phase]
```

---

## 📑 Sample Reconnaissance Report

Below is a template for documenting your findings:

| Category | Information |
| :--- | :--- |
| **Target Domain** | `example.com` |
| **Target IP** | `93.184.216.34` (Resolved via DNS) |
| **DNS Records** | A: 93.184.216.34, MX: mail.example.com, TXT: v=spf1 ... |
| **WHOIS Info** | Registered: 1995, Registrar: ICANN, Name Servers: a.iana-servers.net |
| **Live Hosts** | 192.168.56.101, 192.168.56.102 |
| **Open Ports (TCP)** | 22 (SSH - OpenSSH 7.9), 80 (HTTP - nginx 1.14), 443 (HTTPS - nginx), 3306 (MySQL - 5.7) |
| **Open Ports (UDP)** | 53 (DNS), 123 (NTP) |
| **OS Guess** | Linux 3.x - 5.x (Ubuntu) |
| **Services & Versions** | SSH 7.9p1, nginx 1.14.0, MySQL 5.7.27 |
| **Potential Vulnerabilities** | nginx < 1.16 is vulnerable to CVE-2019-9511. |
| **Notes** | Port 22 exposes password authentication; brute-force risk. |

---

## ⚖️ Ethical & Legal Considerations

> ⚠️ **WARNING:** Unauthorized scanning is illegal in most countries and violates computer fraud laws (e.g., CFAA in the US).

**Golden Rules:**
1.  **Obtain Written Permission:** Always have a signed contract or written authorization before scanning any system you do not own.
2.  **Stay Within Scope:** If the contract says scan only ports 80 and 443, do not scan port 22.
3.  **Respect Privacy:** Be careful with data you discover; don't download or exfiltrate sensitive information without specific permission.
4.  **Use Dedicated Labs:** For practice, use local VMs (Metasploitable, DVWA, OWASP Juice Shop) or platforms like HackTheBox/TryHackMe.

---

## 📸 Proof of Completion

To verify successful completion of this task for your internship portal, provide the following screenshots:

1.  **Network Configuration Check**
    - Kali terminal showing the output of `ip addr` and `ip route`.

2.  **DNS Lookup & WHOIS**
    - Screenshots of `nslookup example.com` and `whois example.com`.

3.  **Connectivity**
    - Output of `ping -c 4 8.8.8.8` or a lab target.

4.  **Authorized Port Scan**
    - Screenshot of `nmap -sV -sS <your-lab-IP>` (e.g., on Metasploitable).
    - Ensure you highlight the open ports and services found.

5.  **NSE Script Execution**
    - (Optional but recommended) Show the output of `nmap --script=vuln <your-lab-IP>`.

---

## 🐞 Troubleshooting & Common Errors

| Issue | Likely Cause | Solution |
| :--- | :--- | :--- |
| **Ping fails** | ICMP is blocked by the firewall. | Use `nmap -sn` (ping sweep) or `nmap -Pn` (treat host as online) to skip ping. |
| **DNS queries timeout** | Misconfigured `/etc/resolv.conf`. | Edit the file: `sudo nano /etc/resolv.conf` and add `nameserver 8.8.8.8`. |
| **Nmap slow scan** | Default timing is too conservative. | Use `-T4` to speed up, but be aware it might be less accurate in congested networks. |
| **"Permission denied" errors** | Trying to use privileged operations (SYN scan). | Run as root: `sudo nmap ...` |
| **No open ports found** | Firewall is dropping packets. | Try `nmap -sT` (TCP connect) instead of `-sS`, or scan a different target. |
| **WHOIS returns privacy info** | Domain uses WHOIS privacy protection. | Use `dnsrecon` or `theHarvester` to find other associations. |

---

## ✅ Conclusion

I have successfully acquired a strong foundation in networking principles, including IP addressing, DNS resolution, port identification, and protocol analysis. 
Furthermore, I have practiced both passive and active reconnaissance techniques using industry-standard tools such as `dig`, `nslookup`, `whois`, `ping`, and `Nmap`. 
By understanding the importance of ethics and authorization, I can apply these skills responsibly in future security assessments.
