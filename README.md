<h1 align="center"> 
   🔐Footprint and Network Scanning <br>
</h1>
<p align="center"
  <b> Reconnaissance of Networkwalks.com and a local network scanning using Kali linux tools and Zenmap </b>
</p>

<p align="center">

<img src="https://img.shields.io/badge/Skill-Cybersecurity-111827?style=flat-square&labelColor=9f1239">

<img src="https://img.shields.io/badge/Ver-VirtualBox%207.2-2563eb?style=flat-square">

<img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-b45309?style=flat-square">

<img src="https://img.shields.io/badge/Skill-footprinting-111827?style=flat-square">

<br>

<img src="https://img.shields.io/badge/Penetration%20Testing-991b1b?style=flat-square">

<img src="https://img.shields.io/badge/Skill-Ethical Hacking-111827?style=flat-square">

<img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github">

<img src="https://img.shields.io/badge/Kali%20Linux-557C94?style=flat-square&logo=kalilinux&logoColor=white">

<br>

<img src="https://img.shields.io/badge/NetworkWalks-7f1d1d?style=flat-square">

<img src="https://img.shields.io/badge/Ethical%20Hacking-9a3412?style=flat-square">

<img src="https://img.shields.io/badge/Oluwatumilara%20Emmanuel%20Opakunbi-991b1b?style=flat-square">

</p>

<hr>

# 🎯 Project Overview
In this project, There are two phases:

1. **Footprinting Networkwalks** using Six built-in Kali tools --- gathering domain, technology DNS, and firewall information from a safe distance.

2. **Local Network Scanning** using Zenmap --- to discover live hosts on the network.
   
<hr>

Reconnaissance is the first step of every attack or authorized security test. All the tools used here are not lethal attack tools; they only extract information that is already available publicly if you know how to look.  

<hr>

## 📌 Objectives
The main objectives of this project are to:
- Find domain registration details using `whois` 
- Fingerprint the web technology using `whatweb`
- Resolve the domain to its IP address using `nslookup`
- Read the HTTP response headers using`curl-I`
- Detect any Web Application firewall using `wafwoof`
- Enumerate all DNS records using `dnsrecon`
- Run **Zenmap** to discover live hosts on a local subnet.
- Compile all findings into a single pentest-style report.  

<hr>

## 🛡️ Scope & Authorization

| Phase | Target | Authorization |
|---|---|---|
| Footprinting (PM1) | `networkwalks.com` | Program's own designated training target -- authorized by Networkwalks for student practice |
|Network Scanning (PM5)| Own Local LAN subnet ( `10.0.0.0/24`),| Own virtual network -- full ownership/authorization|

> ⚠️ Important: These techniques must only be used against systems you own or have explicit written permission to test.

<hr>

# Part 1- Footprinting: networkwalks.com
---
## Task 1- WHOIS: Domain Registeration
---

Command:

```
whois networkwalks.com
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whois%20Screenshot%201.png)

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whois%20Screenshot%202.png)

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whois%20Screenshot%203.png)

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whois%20Screenshot%204.png)

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whois%20Screenshot%205.png)


Findings:
- Registrar: GoDaddy.com, LLC
- Registered: Nov6, 2019
- Expires : Nov 6, 2027
- Name of Servers: NSS6135/NS6136.HOSTGATOR.COM, NS29/NS30.DOMAINCONTROL.COM (hosting → HostGator)
- Registrant identity: privacy-protected via Domains By Proxy, LLC (Tempe, Arizona)
- Abuse contact: abuse@godaddy.com

How attackers use this: Name servers reveal the hosting provider instantly. Registrant privacy hides the real owner, but abuse/registrar details still help with social engineering or abuse reporting. Registration/expiry dates help track domain lifecycle 

---

## Task 2- WhatWeb: Technology Fingerprinting
---
### Command: 
```
whatweb networkwalks.com
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Whatweb.png)

Findings:

- CMS: WordPress 7.1, plugin WP Download Manager 3.3.58
- Server: Apache, IP `192.232.216.135`
- Stack: Bootstrap 7.1, jQuery 3.7.1, HTML5, Google Tag Manager

How attackers use this: Exact WordPress core + plugin versions can be checked against CVE databases for known, exploitable vulnerabilities.

<hr>

# Task 3 — Nslookup: IP Resolution
---
## Command:
```
nslookup networkwalks.com
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/nslookup.png)

Findings: Resolved IP — `192.232.216.135` (queried via DNS server 8.8.8.8)

How attackers use this: Converts the domain to its real IP, enabling direct scanning and infrastructure mapping.

<hr>

# Task 4 — Curl: HTTP Response Headers
---
## Command:
```
curl -I https://networkwalks.com
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Curl%20-I.png)

Findings:

- HTTP/2 200, Server: Apache
- WordPress REST API exposed at `/wp-json/`
- Caching headers: `x-nginx-cache`, `x-endurance-cache-level` (Endurance/HostGator stack)
- Sets `__wpdm_client` cookie (Secure, HttpOnly)

How attackers use this: HTTP headers leak the web server, caching stack, and hidden endpoints (like the REST API) — a common WordPress recon/attack surface — without loading the full page.

<hr>

# Task 5 — Wafw00f: WAF Detection
---
## Command:
```
wafw00f networkwalks.com
``` 

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Wafw00f.png)

Findings: WAF detected — ModSecurity (SpiderLabs)

**How attackers use this**: Confirms a firewall is watching; naive attack attempts will likely be blocked or logged, forcing an attacker to adapt or attempt a bypass.

<hr>

# Task 6 — Dnsrecon: DNS Enumeration

## Command:
```
dnsrecon -d networkwalks.com
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Dnsrecon%20-d%20network%20walks%20.png)

Findings:

- Mail server: mail.networkwalks.com (192.232.216.135)
- DNS software: BIND 9.16.23
- SPF record: v=spf1 +a +mx +ip4:50.87.144.87 include:websitewelcome.com ~all
- 8 SRV records — all _autodiscover._tcp pointing to cPanel email hosts (cpanelemaildiscovery.cpanel.net) → confirms cPanel hosting

How attackers use this: Maps the full DNS footprint — each record (mail server, DNS software version, SPF policy, SRV records) is a potential foothold and reveals the email/hosting setup.

<hr>

# 🪜 Part 2 — Network Scanning: Local LAN (Zenmap)
---
# Task 7 — Ping Scan: Live Host Discovery
---
Command:
```
nmap -sn 10.0.0.0/24
```

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/ping%20Scan%20Screenshot.png)

Findings:

- Subnet scanned: `10.0.0.0/24` (VirtualBox NAT Network)
- Live hosts: 2 (10.0.0.1, 10.0.0.2)
- MAC address: `52:54:00:12:35:00` (QEMU virtual NIC) — visible for the gateway host
- Scan completed in 2.92 seconds (256 IP addresses checked)

How attackers use this: A ping sweep is the fastest way to map which devices are alive on a network before deciding which hosts to probe further.

# Task 8 — Topology View

![image alt](https://github.com/TumilaraEmmanuel/NETWORKWALKS-TUMILARAEMMANUEL-B083-WK2-PM1-PM5-FOOTPRINTING-SCANNING/blob/57e5bfae7fd5e693f7cf3a19cdbff66d6c5abc68/Ping%20Scan%20Topology.png)

Findings: Star topology — localhost at center, connected to 10.0.0.2 , 10.0.0.3, 10.0.0.4 and 10.0.0.5 (own Kali VMs).

<hr>

# 🔎 Summary of Findings
| Tool |	Target |	Key Finding |
|---|---|---|
| whois |	networkwalks.com | GoDaddy registrar, HostGator hosting, privacy-protected owner |
| whatweb	| networkwalks.com	| WordPress 7.1 + WP Download Manager 3.3.58, Apache|
| nslookup	| networkwalks.com	| IP: 192.232.216.135 |
| curl -I	| networkwalks.com	| HTTP/2 200, WordPress REST API exposed |
| wafw00f	| networkwalks.com |	Protected by ModSecurity (SpiderLabs) WAF |
| dnsrecon	| networkwalks.com | BIND 9.16.23, cPanel hosting, 8 SRV records |
| Zenmap (Ping Scan)	| 10.0.0.0/24 (own LAN)	| 4 live hosts found |

<hr>

# 🐞 Problems Encountered & Solutions

### Problem 1. Cloned Virtual machines had same IP4 address and couldn't be pinged from Zenmap Nmap on window 

**Symptoms**: Zenmap Nmap found no live hosts locally on 10.0.0.0/24

**Cause**: Original Kali Linux was clones into 3 different VMs.

**Solution**: 
- The 3 cloned Kali Linux VMs were IP4 addresses were reconfigured to 10.0.0.3, 10.0.0.4 and 10.0.0.5 respectively.
- Mapping was done using Zenmap on Kali Linux

<hr>

# 💡 What I Learned
- Footprinting builds a complete profile of a target using only public information, before any active engagement — this is why it's hard to detect.
- Each tool reveals a different layer: `whois` and DNS tools expose ownership/hosting, `whatweb`/`curl` expose the software stack, wafw00f exposes defenses.
- A single misconfigured plugin/CMS version (seen via `whatweb`) can be the entry point an attacker looks for.
- Network scanning with Zenmap is a fast way to discover live hosts on a subnet — a ping scan alone reveals which devices are worth investigating further.
- Passive recon never touches the target directly, which is why it's the safest and stealthiest phase of a security assessment.

<hr>

# 🔐 Security & Ethical Use
---
This project is intended strictly for educational purposes and authorized security testing as part of the Networkwalks Cybersecurity & Ethical Hacking internship.

>⚠️ Never use these techniques against unauthorized systems, networks, websites, or devices.

<hr>

## 👤 Author
---
Opakunbi Oluwatumilara Emmanuel 
Cybersecurity Intern — Batch B083 Networkwalks

LinkedIn: https://linkedin.com/in/opakunbi-oluwatumilara-79a394210

<hr>

# 📌 Project Information
---
| Field |	Details |
|---|---|
| Program Name	| Cybersecurity at Networkwalks|
|Batch	| B083 |
| Week	| 02 |
| Project	| Footprinting (PM1) + Network Scanning (PM5) + Final Report |
| Targets	| networkwalks.com (footprinting), own LAN 10.0.0.0/24 (scanning) |
| Platform	 | Kali Linux |
| Repository	| GitHub |

<hr>

# 🔐 Learn • Practice • Secure
Cybersecurity Lab — Week 02

<hr>
