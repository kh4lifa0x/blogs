---
title: "Nobitex Breach: $81 Million Theft Under Investigation"
date: 2025-06-18 13:18:21 +0200
categories: [Threat Intelligence]
tags: [kimsuky, nightingale, opsec-failure, threat-actors]
image:
  path: WhatsApp-Image-2025-06-18-at-16.17.19_761d5c43-e1750252765802.jpg
  alt: "Nobitex Breach: $81 Million Theft Under Investigation"
media_subpath: /assets/img/posts/nobitex-breach-81-million-theft-under-investigation
toc: true
---

Iranian Crypto Exchange Nobitex Breached in $81M Heist Attributed to Israel-Linked Threat Actors

![](image-25-1024x503.png)

As the **DarkAtlas** Research Squad, we conducted a thorough investigation to uncover the root cause behind the Nobitex breach.

Our investigation reveals that **two Nobitex employees with elevated server access were compromised via infostealer malware campaigns**. These infostealers—malicious tools crafted to extract sensitive information such as credentials, browser history, and session cookies—have become a favored method among cybercriminals.

The logs associated with the malware campaigns contain a trove of compromised Nobitex-related data, including:

- **Webmail credentials** for Nobitex’s email server (`bitex-mail.nobitex.net/owa/`)
- **Administrative credentials** for internal systems (`admin.nxbo.ir`)
- **Corporate testnet credentials** (`testnet.nobitex.ir`)
- **JIRA platform login details** (`jira.nxbo.ir/login.jsp`)
- **Cookies** associated with various internal Nobitex platforms

**Infected employee** #1

**On September 20, 2024**, an Iranian workstation was compromised by the **StealC infostealer malware**. Analysis of the exfiltrated data indicates that the infected machine belonged to a **developer at Nobitex**, and contained multiple sets of **corporate credentials** granting **sensitive access to internal infrastructure**.

![](image-27-1024x84.png)

The compromised user’s role at **Nobitex** has been identified as a **Front-end Developer**. This attribution is based on autofill data recovered from the infected system, which includes profile information explicitly listing the role as *“Front-end developer @ Nobitex”* along with associated organizational email addresses (e.g., `***@nobitex.net`).

---

**Infected employee** #2

On **September 15, 2023**, a second Iranian workstation was compromised, this time by the **RedLine Infostealer**. Analysis of the exfiltrated data indicates that the infected device belonged to a **Nobitex employee**. Recovered logs contain multiple sets of **corporate credentials** associated with Nobitex’s internal infrastructure, suggesting that this employee had access to critical parts of the organization’s network.

![](image-28-1024x250.png)

As the **Nobitex breach** illustrates, cryptocurrency exchanges cannot afford to underestimate the **stealthy and destructive nature of infostealers**. These malware strains silently compromise employee endpoints, often serving as the initial access vector for large-scale intrusions.

Following the breach, **Nobitex suspended operations and pledged user compensation**, yet the reputational and operational fallout is already severe. Even more alarming is the **threat from attackers to leak internal source code**, which—if released—could expose deeper architectural flaws and open the door to future exploitation.

This incident closely mirrors other high-profile compromises, such as the **Lazarus Group’s alleged infiltration of Bybit**, where **initial access was also linked to credential theft**. These cases collectively highlight a growing pattern: **threat actors are increasingly targeting employees, not infrastructure, to bypass defenses and stage devastating attacks.**

**Conclusion**

**Infostealers represent a rapidly escalating threat**, empowering cybercriminals to execute high-impact breaches against major organizations. By targeting weak points such as **webmail portals**, **VPN access**, and **autofill-stored credentials**, these malware strains provide attackers with immediate entry into corporate environments—often bypassing perimeter defenses entirely. This tactic has been observed in multiple recent intrusions affecting prominent companies.
