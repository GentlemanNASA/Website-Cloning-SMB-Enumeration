# Website Cloning & SMB Enumeration

A hands-on offensive security lab demonstrating two common attack vectors: credential harvesting through website cloning using the Social-Engineer Toolkit (SET), and SMB share enumeration on a target host.

Conducted as part of the ParoCyber ethical hacking program in a controlled, authorized lab environment.

---

## Lab Overview

This lab covers two distinct attack techniques that are commonly used during the reconnaissance and initial access phases of a penetration test:

**Part 1 — Website Cloning (SET)**
Using the Social-Engineer Toolkit to clone a legitimate website and serve it locally as a phishing vector. The goal is to understand how attackers harvest credentials through lookalike pages, and how an HTML redirect can silently forward victims after form submission.

**Part 2 — SMB Enumeration**
Using Nmap NSE scripts and smbclient to identify and enumerate SMB shares on a target host, simulating what an attacker would do after gaining initial network access.

---

## Tools Used

| Tool | Purpose |
|---|---|
| Social-Engineer Toolkit (SET) | Website cloning and credential harvesting |
| Apache / Python HTTP Server | Serving the cloned page |
| Nmap | SMB port scanning and share enumeration |
| smbclient | Manual SMB share verification |
| Kali Linux | Attack platform |

---

## Environment

- Operating System: Kali Linux
- Lab Network: Internal ParoCyber training environment
- Target: Authorized lab host
- All activities performed under written authorization

---

## Part 1: Website Cloning with SET

### How it works

SET's credential harvester module clones a target website and hosts it on the attacker's machine. When a victim submits a form, credentials are captured server-side and the victim is redirected to the real site — making the attack nearly invisible.

### Steps performed

1. Launched SET as root
2. Selected: Social-Engineering Attacks → Website Attack Vectors → Credential Harvester → Site Cloner
3. Entered the attacker's IP to receive POST data
4. Entered the target URL to clone
5. SET cloned the page and started listening
6. Simulated a victim visiting the cloned page and submitting credentials
7. Observed captured credentials in the SET console
8. Verified the HTML redirect forwarding the victim back to the original site

### Key takeaway

This demonstrates why URL verification and HTTPS certificate inspection are critical for end users. A cloned page served over HTTP with a convincing domain name is difficult to distinguish from the real thing at first glance.

---

## Part 2: SMB Enumeration

### How it works

SMB (Server Message Block) is a network protocol used for file sharing. Misconfigured SMB shares are a common finding in internal penetration tests and can expose sensitive files or allow lateral movement.

### Steps performed

```bash
# Scan SMB ports
nmap -A -p139,445 <target>

# Enumerate SMB shares using NSE script
nmap --script smb-enum-shares.nse -p445 <target>

# Manually verify share access
smbclient //<target>/print$ -N
```

### Key takeaway

Unauthenticated SMB enumeration can reveal share names, permissions, and sometimes file listings without any credentials. Disabling guest access and enforcing SMBv3 with signing are standard hardening measures.

---

## Documentation

Full lab documentation including screenshots and observations is available in the attached PDF.

---

## Disclaimer

All activities in this lab were performed in an authorized, isolated environment as part of a structured cybersecurity training program. This repository is intended for educational purposes only. Never attempt these techniques on systems you do not own or have explicit written permission to test.

---

## Author

[GentlemanNASA](https://github.com/GentlemanNASA) — Cybersecurity student, ParoCyber ethical hacking program.
