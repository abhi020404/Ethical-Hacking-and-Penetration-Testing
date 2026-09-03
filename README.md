# 🛡️ Ethical Hacking & Penetration Testing Lab

> **A hands-on cybersecurity practical project covering Reconnaissance, Scanning, Exploitation, Post-Exploitation, Password Security, Phishing Awareness, Malware Analysis and System Hardening.**

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red?style=for-the-badge)
![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-blue?style=for-the-badge\&logo=kalilinux)
![Metasploit](https://img.shields.io/badge/Tool-Metasploit-orange?style=for-the-badge)
![Nmap](https://img.shields.io/badge/Tool-Nmap-4B8BBE?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 📌 Overview

This repository contains documentation and practical work for an **Ethical Hacking & Penetration Testing assignment** performed in an isolated and authorized cybersecurity lab.

The project demonstrates how a penetration tester can identify security weaknesses, validate vulnerabilities in a controlled environment, assess the potential impact, and recommend defensive mitigations.

The practical workflow follows:

```text
Reconnaissance
      ↓
Scanning
      ↓
Vulnerability Identification
      ↓
Controlled Exploitation
      ↓
Initial Access
      ↓
Post-Exploitation
      ↓
Password Security Audit
      ↓
Security Awareness
      ↓
Malware Analysis
      ↓
System Hardening
      ↓
Reporting
```

---

## 🎯 Objectives

The main objectives of this project are to:

* Understand the penetration-testing lifecycle
* Perform network reconnaissance
* Identify exposed ports and services
* Enumerate service versions
* Validate a known vulnerability in a deliberately vulnerable machine
* Establish controlled lab access
* Perform basic post-exploitation validation
* Demonstrate password-security weaknesses
* Understand phishing and social-engineering risks
* Study static and dynamic malware-analysis concepts safely
* Apply basic system-hardening controls
* Document security findings and recommended mitigations

---

## 🧪 Lab Environment

| Component        | Configuration                            |
| ---------------- | ---------------------------------------- |
| Attacker Machine | Kali Linux                               |
| Target Machine   | Metasploitable2                          |
| Virtualization   | VirtualBox                               |
| Network          | Isolated Host-Only / Private Lab Network |
| Testing Type     | Authorized Security Testing              |
| Primary Focus    | Penetration Testing                      |

### Lab Architecture

```text
┌───────────────────────┐
│      Kali Linux       │
│   Security Testing    │
│                       │
│ Nmap / Metasploit     │
│ Hydra / John / etc.   │
└───────────┬───────────┘
            │
            │ Isolated Lab Network
            │
┌───────────▼───────────┐
│     Metasploitable2   │
│   Intentionally       │
│   Vulnerable Target   │
└───────────────────────┘
```

> ⚠️ **Important:** All offensive-security activities documented in this repository are intended only for an authorized, isolated laboratory environment.

---

# 🔎 1. Reconnaissance

The first phase focused on understanding the lab network and confirming communication between the testing machine and the intentionally vulnerable target.

### Activities

* Identify Kali Linux network configuration
* Identify target IP address
* Verify connectivity
* Confirm that both virtual machines are on the same isolated network

Example:

```bash
ip addr
```

Target-side:

```bash
ifconfig
```

Connectivity test:

```bash
ping -c 4 <TARGET_IP>
```

### Objective

The goal of reconnaissance is to establish the correct target scope before performing any security testing.

---

# 🛰️ 2. Network Scanning

Nmap was used to identify reachable ports and exposed services.

Example:

```bash
nmap -sV <TARGET_IP>
```

For operating-system detection:

```bash
nmap -sV -O <TARGET_IP>
```

### Information collected

* Open ports
* Running services
* Service versions
* Potential attack surface
* Possible vulnerable services

### Why this matters

An exposed service increases the attack surface of a system. Service enumeration helps a security tester determine which components require further investigation.

---

# 💥 3. Vulnerability Validation with Metasploit

The Metasploit Framework was used to validate a known vulnerability against the deliberately vulnerable Metasploitable2 machine.

Example module:

```text
exploit/multi/samba/usermap_script
```

Basic workflow:

```text
use exploit/multi/samba/usermap_script
        ↓
show options
        ↓
set RHOSTS <TARGET_IP>
        ↓
set LHOST <KALI_IP>
        ↓
run
```

The objective was to demonstrate how a known vulnerability can potentially provide initial access to an intentionally vulnerable system.

> This repository does not target production systems or third-party infrastructure.

---

# 🖥️ 4. Reverse Shell & Initial Access

A controlled reverse connection was demonstrated inside the isolated lab.

Conceptually:

```text
Metasploitable2
      │
      │ Reverse Connection
      ▼
Kali Linux Listener
      │
      ▼
Controlled Shell Session
```

After a successful session, basic system information can be validated.

Example commands:

```bash
whoami
uname -a
pwd
ls
```

The purpose is to understand the security impact of successful exploitation without performing unnecessary actions on the target.

---

# 🔐 5. Post-Exploitation

Post-exploitation activities were limited to basic validation of the obtained session.

Typical information includes:

```text
System information
Current user
Architecture
Working directory
Basic filesystem information
```

For a compatible Meterpreter session:

```text
sysinfo
getuid
```

The objective is to demonstrate the difference between:

> **Initial Access → Understanding Access → Assessing Impact**

---

# 🔑 6. Password Security Audit

Password security was evaluated using controlled lab credentials.

## Hydra

Hydra can be used to demonstrate the risk of weak SSH authentication.

Example:

```bash
hydra -l <LAB_USER> -P ssh-test.txt ssh://<TARGET_IP>
```

The password list used for this exercise should contain only test credentials created for the lab.

### Security Lessons

Weak passwords can increase the likelihood of account compromise.

Recommended defenses:

* Strong unique passwords
* Multi-factor authentication
* SSH key authentication
* Login rate limiting
* Account lockout controls
* Monitoring of repeated authentication failures

---

# 🧩 7. Offline Password Hash Auditing

John the Ripper was used to demonstrate password-hash auditing against a controlled lab hash file.

Example:

```bash
john hashes.txt
```

To display recovered test credentials:

```bash
john --show hashes.txt
```

### Important

Never upload:

* Real passwords
* Production password hashes
* API keys
* Private keys
* Authentication tokens
* Personal credentials

Only synthetic or intentionally created lab data should be used.

---

# 🎣 8. Phishing Awareness Simulation

A credential-free phishing-awareness simulation was created to demonstrate common social-engineering indicators.

### Example indicators

* Urgent language
* Suspicious links
* Unexpected account-verification requests
* Unknown senders
* Mismatched URLs
* Requests for sensitive information

### Awareness Message

```text
STOP → CHECK → VERIFY

Before clicking:

1. Check the sender
2. Inspect the URL
3. Look for urgency or threats
4. Never share passwords or OTPs
5. Verify through an official channel
```

The simulation does **not** collect or transmit credentials.

---

# 🦠 9. Malware Basics

The project also covers basic malware-analysis methodology using a **benign sample in an isolated environment**.

## Static Analysis

Example:

```bash
file sample
```

Calculate the SHA-256 hash:

```bash
sha256sum sample
```

Inspect readable strings:

```bash
strings sample
```

## Dynamic Analysis

Dynamic analysis involves observing the behavior of a sample while it executes inside a controlled sandbox.

Potential observations include:

* Processes
* Filesystem changes
* Network connections
* Registry/configuration changes
* System calls
* Persistence behavior

> Only benign or intentionally provided training samples should be used.

---

# 🛡️ 10. System Hardening

The final phase focused on reducing the attack surface.

## Update Packages

```bash
sudo apt update
sudo apt upgrade
```

## Firewall

Check firewall status:

```bash
sudo ufw status
```

Enable UFW where appropriate:

```bash
sudo ufw enable
```

## Review Listening Services

```bash
sudo ss -tulpn
```

## Review Running Services

```bash
systemctl list-units --type=service --state=running
```

Unused services should be disabled only after confirming that they are not required.

---

# 📊 11. Security Findings

| ID   | Finding                          | Severity    | Recommended Action              |
| ---- | -------------------------------- | ----------- | ------------------------------- |
| F-01 | Vulnerable legacy service        | 🔴 Critical | Patch, upgrade or remove        |
| F-02 | Weak authentication risk         | 🟠 High     | Strong passwords + MFA          |
| F-03 | Excessive exposed services       | 🟡 Medium   | Reduce attack surface           |
| F-04 | Phishing/social-engineering risk | 🟡 Medium   | Security awareness training     |
| F-05 | Missing/insufficient hardening   | 🟠 High     | Patch and apply secure baseline |

---

# 📸 12. Evidence & Screenshots

The final report contains illustrative screenshots for demonstrating the expected workflow.

For a formal practical submission, screenshots should be replaced with **actual screenshots captured from the authorized lab environment**.

Recommended evidence:

```text
screenshots/
├── 01-network-config.png
├── 02-ping.png
├── 03-nmap-scan.png
├── 04-metasploit-options.png
├── 05-exploitation-session.png
├── 06-post-exploitation.png
├── 07-hydra-audit.png
├── 08-john-audit.png
├── 09-phishing-awareness.png
├── 10-malware-analysis.png
└── 11-hardening.png
```

---

# 📁 13. Repository Structure

```text
apexplanet-ethical-hacking-assignment/
│
├── README.md
│
├── reconnaissance/
│   ├── network-discovery.md
│   └── screenshots/
│
├── scanning/
│   ├── nmap-scan.md
│   └── screenshots/
│
├── exploitation/
│   ├── metasploit.md
│   └── screenshots/
│
├── post-exploitation/
│   ├── session-analysis.md
│   └── screenshots/
│
├── password-auditing/
│   ├── hydra.md
│   ├── john-the-ripper.md
│   └── screenshots/
│
├── phishing-awareness/
│   ├── awareness-page/
│   └── README.md
│
├── malware-analysis/
│   ├── static-analysis.md
│   └── dynamic-analysis.md
│
├── hardening/
│   ├── firewall.md
│   ├── patching.md
│   └── services.md
│
├── report/
│   └── ApexPlanet_Ethical_Hacking_Practical_Report.pdf
│
└── demo/
    └── demo-video.md
```

---

# 📄 14. Project Report

The complete practical report is available here:

➡️ **[Ethical Hacking Practical Report](./report/ApexPlanet_Ethical_Hacking_Practical_Report.pdf)**

The report covers:

* Lab setup
* Reconnaissance
* Nmap scanning
* Metasploit exploitation
* Reverse shell
* Post-exploitation
* Hydra
* John the Ripper
* Phishing awareness
* Malware-analysis concepts
* System hardening
* Findings
* Mitigations
* Evidence register
* Demonstration plan

---

# 🎥 15. Demonstration Video

The project demonstration follows this structure:

```text
00:00 → Introduction
00:45 → Lab Architecture
02:00 → Reconnaissance & Nmap
04:00 → Vulnerability Validation
05:00 → Reverse Shell
06:00 → Post-Exploitation
07:00 → Password Security
08:00 → Phishing Awareness
09:00 → Malware Analysis
09:30 → Hardening & Conclusion
```

---

# 🧠 Key Learnings

Through this project, I learned that cybersecurity is not simply about exploiting vulnerabilities.

The complete security process is:

```text
Find the Weakness
       ↓
Understand the Risk
       ↓
Validate Safely
       ↓
Document Evidence
       ↓
Fix the Vulnerability
       ↓
Harden the System
       ↓
Continuously Monitor
```

The biggest takeaway:

> **A vulnerability becomes a serious security issue when it can be chained with other weaknesses to increase impact.**

---

# 🛡️ Security & Responsible Use

This repository is intended strictly for:

* Education
* Authorized penetration testing
* Cybersecurity training
* Local laboratory environments
* Security awareness

Do **not** use the techniques documented here against systems without explicit authorization.

Never target:

* Public websites without permission
* Third-party servers
* Personal devices
* Production infrastructure
* Accounts that you do not own or have permission to test

The author is not responsible for unauthorized or malicious use of the information contained in this repository.

---

# 📚 References

* [GitHub README Documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
* [GitHub Repository Best Practices](https://docs.github.com/en/repositories/creating-and-managing-repositories/best-practices-for-repositories)
* [Kali Linux](https://www.kali.org/)
* [Metasploit](https://www.metasploit.com/)
* [Nmap](https://nmap.org/)
* [Openwall John the Ripper](https://www.openwall.com/john/)

---

video link : https://lnkd.in/p/gb9CYbxK
