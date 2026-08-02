---
title: "DragonForce Ransomware: From Hacktivism to Global Cyber Extortion"
date: 2025-06-29 08:58:09 +0200
categories: [Ransomware]
tags: [ransomware]
image:
  path: dragonforce-ransomware-4-min.png
  alt: "DragonForce Ransomware: From Hacktivism to Global Cyber Extortion"
media_subpath: /assets/img/posts/dragonforce-ransomware-from-hacktivism-to-global-cyber-extortion
toc: true
---

**DragonForce Ransomware** emerged in 2023 as a formidable threat within the cybercriminal landscape, operating under a *Ransomware-as-a-Service (RaaS)* model. Initially, the group—also named *DragonForce*—made headlines through ideologically driven cyberattacks, strategically targeting organizations whose values opposed their political stance. However, the group has since evolved, shifting toward financially motivated operations and establishing itself as a key player in the global ransomware ecosystem.

Leveraging a RaaS infrastructure, **DragonForce** empowers affiliates with a sophisticated and modular toolkit, enabling them to craft and deploy tailored ransomware payloads. This flexibility has allowed affiliates to strike across a broad spectrum of industries. The group’s campaigns have notably impacted high-value targets in the **retail**, **financial**, and **manufacturing** sectors, with widespread incidents reported across **North America**, **Europe**, and **Asia**.

**DragonForce first appeared in December 2023** with the debut of its *“DragonLeaks”* dark web portal, serving as a centralized hub for data leaks, victim shaming, and ransom negotiations. Some analysts trace the group’s origins to *DragonForce Malaysia*, a well-known hacktivist collective, suggesting ideological roots. However, DragonForce’s current trajectory signals a clear shift—from activism to monetized cybercrime.

By 2025, the group has evolved into a mature ransomware operation with a highly organized Ransomware-as-a-Service (RaaS) model, designed to attract both displaced affiliates from dismantled ransomware crews and freelance threat actors seeking robust infrastructure.

**Key features of DragonForce’s RaaS platform include:**

- **Customizable Payload Builder:** Affiliates can tailor encryption modules, ransom notes, and lateral movement behavior to fit the target environment.
- **Stealth-Optimized Encryption:** The malware employs intermittent encryption and evasion techniques to bypass EDR and anti-ransomware defenses.
- **Multilingual Victim Portals:** The leak site and ransom negotiation platforms are localized for global impact, facilitating communication with international victims.
- **Robust Affiliate Support:** DragonForce provides documentation, technical assistance, and even crypto-laundering guidance, mirroring a SaaS-like experience.
- **Tiered Revenue Sharing Model:** Earnings are split based on affiliate ranking, incentivizing more destructive and high-value campaigns.

![](image-32.png)

---

**DragonForce** vs. **RansomHub: A Glimpse into RaaS Turf Wars**

On **April 1st, 2025**, the *RansomHub* data leak site (DLS) abruptly went offline, and affiliate communications reportedly ceased—prompting frustration and speculation within cybercriminal underground forums. Affiliates voiced concerns over the group’s sudden disappearance, fueling rumors of operational failure or internal sabotage.

The very next day, on **April 2nd, 2025**, ***DragonForce*** seized the moment. In a publicly posted announcement, the group “invited” **RansomHub** to join their infrastructure—a move many interpreted not as a genuine offer, but as a thinly veiled taunt. The timing and tone suggested **DragonForce** was capitalizing on **RansomHub’s** apparent collapse, using it as an opportunity to assert dominance in the competitive Ransomware-as-a-Service (RaaS) market.

![](image-33.png)

---

![](image-41-1024x540.png)

On **April 23rd, 2025**, *“koley”*—the spokesperson for *RansomHub*—resurfaced on underground forums after weeks of silence. In their message, koley claimed that RansomHub had suffered a **state-sponsored cyberattack**, and publicly identified an alleged **traitor** from within their own ranks, hinting at internal sabotage.

Just two days later, on **April 25th**, koley escalated the drama by posting a screenshot showing that *DragonForce’s* own Data Leak Site (DLS) had been **compromised and defaced**. The defacement included a cryptic message implying that the breach was orchestrated from the inside—again by **“traitors.”**

![](image-34.png)

---

On **April 28th, 2025**, ***DragonForce*** posted an update on the same underground forum thread where they previously advertised their Ransomware-as-a-Service (RaaS) offering. In the post, they announced a temporary **pause on accepting new collaborators**, citing “recent events” as the reason.

![](image-35.png)

---

Based on current chatter across underground forums, two dominant theories have emerged regarding the recent chaos involving ***RansomHub*** and ***DragonForce***:

1. **RansomHub Pulled an Exit Scam — and May Be DragonForce Rebranded:**  
   Some speculate that *RansomHub’s sudden disappearance*, followed by *DragonForce’s rise* and mocking commentary, may not be a coincidence. The theory suggests RansomHub executed a planned **exit scam**, liquidated earnings, and resurfaced under the *DragonForce* brand with new infrastructure and a modified public image. The resurfacing of *koley* could be an attempt to muddy the waters or distance themselves from the new brand while retaining some operational control.
2. **DragonForce and RansomHub Are Rivals Locked in Escalating Hostilities:**  
   An alternative theory suggests that the two groups are **competing RaaS operators**, and the recent events reflect a **deepening turf war**. From infrastructure outages to retaliatory defacements and accusations of betrayal, the unfolding events point toward an increasingly hostile rivalry. DragonForce’s decision to pause new affiliate onboarding further supports the idea of internal unrest and the fallout of cybercriminal infighting.

![](image-36.png)
![](image-37.png)

---

**DragonForce Ransomware’s Techniques**

When *DragonForce Ransomware* first emerged, it was observed leveraging a **leaked ransomware builder attributed to LockBit 3.0 (aka LockBit Black)**—the third generation of the prolific LockBit ransomware family. Originally developed by the LockBit group, LockBit 3.0 introduced advanced features such as modular payloads, faster encryption, and stronger obfuscation techniques. However, in **September 2022**, a disgruntled developer leaked the builder, resulting in widespread adoption by unaffiliated threat actors.

**DragonForce** is among the groups that capitalized on this leak, using the stolen builder as a foundation for their early operations. This allowed them to rapidly deploy **sophisticated ransomware campaigns** without investing in ground-up malware development.

Like many modern RaaS operators, **DragonForce** employs a **double extortion model**: they not only encrypt the victim’s systems but also **exfiltrate sensitive data**. Victims are threatened with the public release of stolen data via **DragonForce**’s **Data Leak Site (DLS)** if ransom demands are not met—amplifying pressure through reputational and regulatory consequences.

![](Screenshot_28-1024x549.png)

---

**Initial Access and Post-Exploitation Tactics**

*DragonForce affiliates* employ a range of initial access vectors to infiltrate target environments. These commonly include:

- **Phishing campaigns** with weaponized attachments or links,
- **Exploitation of publicly known vulnerabilities**, notably **Log4Shell (CVE-2021-44228)**,
- **Brute-force and credential stuffing attacks** against exposed **Remote Desktop Protocol (RDP)** and **VPN services**,
- **Direct access using compromised credentials** obtained from infostealers or previous breaches.

Following successful entry, affiliates typically engage in **post-exploitation activities** using a well-established toolset:

- **Cobalt Strike** for beacon deployment, lateral movement, and staging further payloads,
- **Mimikatz** for extracting plaintext passwords, hashes, and tokens,
- **SystemBC** for establishing persistent command-and-control (C2) via encrypted tunneling.

Internal network traversal is facilitated through **RDP lateral movement** and the exploitation of **inherent trust relationships**, allowing attackers to escalate privileges and prepare for ransomware deployment.

---

### **Affiliate Platform Overview**

DragonForce operates a **centralized affiliate platform** designed to streamline operations for its Ransomware-as-a-Service (RaaS) model. Each affiliate receives access to a **unique .onion-based control panel**, where they operate independently under a dedicated profile.

Core features of the platform include:

**Revenue tracking**: Built-in dashboards display ransom payments and affiliate shares, supporting a **tiered commission model**.

**Payload customization**: Affiliates can tailor ransomware binaries based on target environment and encryption preferences.

**Victim management**: A CRM-like interface enables tracking of compromised organizations, ransom negotiations, and status monitoring.

**Data leak integration**: Direct publication of exfiltrated data to the group’s **DragonLeaks DLS** for public shaming and extortion leverage.

![](image-38-1024x547.png)

---

**DragonForce Ransomware’s Targets**

The *DragonForce* ransomware group has demonstrated a **diverse targeting strategy**, impacting both public and private sector organizations across multiple geographic regions. While opportunistic in some cases, the group’s overall campaign behavior reflects **strategic prioritization of high-impact, disruption-sensitive industries.**

#### **Most Targeted Sectors**

**1. Manufacturing**  
The most consistently targeted sector by DragonForce affiliates, manufacturing encompasses a wide range of organizations—from **electronics and metal fabrication** to **aerospace components** and **industrial machinery producers**. These entities are attractive due to their **tight production timelines**, **just-in-time supply chains**, and the **high cost of downtime**, making them more likely to pay ransoms quickly.

**2. Technology**  
This category includes **IT service providers, telecom firms, and software vendors**. DragonForce likely views these as **force multipliers**, where compromising a single MSP or telecom can cascade to multiple downstream clients.

**3. Construction and Infrastructure**  
Large **construction firms and infrastructure development companies** have become frequent victims, likely due to their growing reliance on interconnected project management platforms and third-party vendors, often with **weaker security controls**.

#### **Other Notable Targets**

- **Healthcare:** Hospitals, specialty clinics, and care centers have been targeted for their sensitive patient data and critical service availability.
- **Logistics & Transportation:** Attacks on distribution centers, freight companies, and transit systems disrupt global and regional supply chains.
- **Legal & Consulting Services:** Law firms and advisory entities often handle confidential data, making them lucrative targets for data exfiltration-based extortion.
- **Retail & Consumer Goods:** Particularly **e-commerce platforms** and **distribution centers**, where downtime translates directly into lost revenue and customer trust.
- **Public Services:** Atypical for many RaaS operations, DragonForce has also targeted **funeral homes, religious institutions**, and **municipal offices**, signaling either a lack of operational restraint or an intent to test soft targets for extortion leverage.

![](image-39-1024x683.png)
![](image-40-1024x683.png)

---

### **Conclusion**

The *DragonForce* ransomware group has swiftly established itself as a **high-impact threat actor** within the global cyber threat landscape. This rise is largely attributed to their dual use of **two powerful ransomware variants**: a repurposed version of **LockBit**, and a **heavily customized fork of Conti**. Notably, the Conti variant incorporates advanced capabilities such as:

- **Sophisticated encryption routines**,
- The ability to **disable EDR/XDR protections** via the **Bring Your Own Vulnerable Driver (BYOVD)** technique,
- And robust **anti-analysis mechanisms** designed to evade forensic and sandbox environments.

These technical enhancements significantly raise the bar for detection and mitigation, particularly for security teams lacking deep threat visibility.

Compounding the threat is the group’s integration of **SystemBC**, a multifunctional malware that provides persistent access, supports **network reconnaissance**, and facilitates **covert lateral movement** within victim environments. This toolchain amplifies the group’s ability to operate stealthily and sustain access during prolonged attack campaigns.

DragonForce’s consistent targeting of **critical infrastructure sectors**—including **manufacturing, real estate, and transportation**—suggests a calculated focus on industries where operational disruption translates directly to financial leverage.

As their tradecraft evolves, DragonForce demonstrates the convergence of **professional RaaS operations** with **APT-like sophistication**, making them a **priority concern for defenders worldwide**. To counter this threat, organizations must:

- Harden external exposure points (e.g., RDP, VPNs),
- Monitor for known DragonForce TTPs using frameworks like **MITRE ATT&CK**,
- Deploy behavioral and threat-informed defenses,
- And foster **incident response readiness** for ransomware-specific scenarios.

---

### MITRE ATT&CK Details:

| Tactic | ID | Description |
| --- | --- | --- |
| Initial Access | Exploit Public-Facing Application (T1190) | DragonForce may exploit vulnerabilities in public-facing applications to gain initial access to the target system. Although not explicitly mentioned, this is common in ransomware. |
| Execution | User Execution (T1204) | DragonForce is delivered via phishing campaigns, where the victim is tricked into opening a malicious attachment (e.g., Word or Excel file) or clicking a malicious link, triggering the execution of the ransomware. |
| Defense Evasion | Indicator Removal on Host (T1070) | DragonForce disables or removes antivirus software, deletes system logs, and erases indicators to avoid detection by security tools. |
| Defense Evasion | Obfuscated Files or Information (T1027) | DragonForce obfuscates its payload by packing or encrypting parts of the code to evade detection and hinder static analysis. |
| Defense Evasion | Impair Defenses (T1562) | DragonForce clears event logs and uses other techniques to disable or remove defenses, such as antivirus software, in order to evade detection. |
| Defense Evasion | Disabling Security Tools (T1089) | DragonForce disables security tools, particularly antivirus software, to facilitate its persistence and to remain undetected. |
| Discovery | System Information Discovery (T1082) | DragonForce gathers system information such as the operating system version, architecture, and installed applications to identify vulnerable targets. |
| Discovery | File and Directory Discovery (T1083) | DragonForce explores file and directory structures to identify valuable files for encryption, which is typical behavior for ransomware. |
| Collection | Archive Collected Data (T1560) | DragonForce collects sensitive data such as user credentials, system configurations, and network information, storing it in a log file for future exploitation. |
| Impact | Data Encrypted for Impact (T1486) | DragonForce uses encryption algorithms, such as AES-256 or RSA, to lock files and demands a ransom for their decryption. |
| Command and Control | Application Layer Protocol (T1090) | DragonForce may use proxy or tunneling techniques to hide its communication with attackers, maintaining control over the infected machine while evading detection. |
| Execution | Remote File Copy (T1105) | DragonForce replicates itself in various directories and may copy itself to other systems on the network after gaining initial access. |
