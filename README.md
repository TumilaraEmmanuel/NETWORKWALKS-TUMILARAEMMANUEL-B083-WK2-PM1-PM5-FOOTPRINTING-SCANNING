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

## 🎯 Project Overview
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

<hr>

## 🛡️ Scope & Authorization

| Phase | Target | Authorization |
|---|---|---|
| Footprinting (PM1) | `networkwalks.com` | Program's own designated training target -- authorized by Networkwalks for student practice |
|Network Scanning (PM5)| Own Local LAN subnet ( `10.0.0.0/24`),| Own virtual network -- full ownership/authorization|

<hr>

<hr>

# Part 1- Footprinting: networkwalks.com
---
##Task 1- WHOIS: Domain Registeration
---
command:
`whois networkwalks.com`



Findings:
- Registrar: Godaddy.com,LLC
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
`whatweb networkwalks.com`


Findings:

- CMS: WordPress 7.1, plugin WP Download Manager 3.3.58
- Server: Apache, IP 192.232.216.135
- Stack: Bootstrap 7.1, jQuery 3.7.1, HTML5, Google Tag Manager

How attackers use this: Exact WordPress core + plugin versions can be checked against CVE databases for known, exploitable vulnerabilities.

<hr>

# Task 3 — Nslookup: IP Resolution
---
## Command:
`nslookup networkwalks.com`


Findings: Resolved IP — `192.232.216.135` (queried via DNS server 8.8.8.8)

How attackers use this: Converts the domain to its real IP, enabling direct scanning and infrastructure mapping.

<hr>

# Task 4 — Curl: HTTP Response Headers
---
## Command:
`curl -I https://networkwalks.com`


Findings:

- HTTP/2 200, Server: Apache
- WordPress REST API exposed at `/wp-json/`
- Caching headers: `x-nginx-cache`, `x-endurance-cache-level` (Endurance/HostGator stack)
- Sets `__wpdm_client` cookie (Secure, HttpOnly)
How attackers use this: HTTP headers leak the web server, caching stack, and hidden endpoints (like the REST API) — a common WordPress recon/attack surface — without loading the full page.

<hr>
