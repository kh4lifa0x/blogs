---
title: "Threat Profile: Conti Ransomware Group"
date: 2025-09-29 08:46:41 +0200
categories: [Threat Intelligence]
tags: [conti, ransomware, threat-actors]
image:
  path: Conti-ransomware.jpg
  alt: "Threat Profile: Conti Ransomware Group"
media_subpath: /assets/img/posts/threat-profile-conti-ransomware-group
toc: true
---

**Executive Summary**

**Conti ransomware**, first identified in **2019**, quickly became one of the most notorious ransomware operations due to its advanced encryption, rapid lateral movement, and use of **double extortion** tactics. Operated as a **Ransomware-as-a-Service (RaaS)** by the **Russia-based Wizard Spider group**, Conti is believed to have evolved from **Ryuk** ransomware and maintained suspected ties to Russian state interests.

Between **2019** and **2022**, Conti carried out large-scale attacks against **healthcare providers, governments, educational institutions, critical infrastructure, and private businesses**, earning an estimated **$180 million in 2021 alone**. Its aggressive tactics and global impact highlighted the urgent need for strong **cybersecurity defenses** and incident response planning.

In **2022**, Conti faced internal divisions following leaked private chats, raising doubts about its future. Despite this, Conti remains a landmark example of modern ransomware operations, demonstrating how **cybercriminal groups operate with the scale, structure, and efficiency of organized enterprises.**

---

**Conti Attack in Action**

Although Conti is often classified as a **Ransomware-as-a-Service (RaaS)** operation, its business model differs slightly from most variants. Instead of affiliates receiving a percentage of ransom payments, reports suggest that Conti paid its initial access brokers a fixed wage. Once access is obtained, the core operators take over and execute the attack using highly aggressive and methodical techniques.

---

Initial Access

**Spearphishing Campaigns:** Customized emails with malicious links or weaponized attachments (often documents embedded with scripts) that drop loaders like **TrickBot** or **Cobalt Strike**, enabling deeper infiltration.

**RDP Exploitation:** Using stolen or weak Remote Desktop Protocol credentials to gain direct access to internal systems.

**Access-as-a-Service Purchases:** Buying entry from **network access brokers** who have already compromised an organization.

---

Lateral Movement and Persistence

**Backdoors & C2:** Deployment of secondary backdoor malware to establish persistent connections with Conti’s command-and-control servers.

**Penetration Tools:** Use of **Cobalt Strike beacon**, **AdFind** (for Active Directory enumeration), and **SMB exploitation** to move laterally and encrypt files across the domain.

**Defense Evasion:** Actively detecting and disabling security tools, and checking for sandbox environments to avoid analysis.

**Credential Access:** Launching **Kerberos ticket attacks**, brute force attempts, and password harvesting for deeper domain control.

**Surveillance:** Monitoring email communications to anticipate victim response strategies, giving Conti leverage during ransom negotiations.

---

Encryption and Destruction

**Multi-threaded Encryption:** Enables fast, large-scale encryption while minimizing noticeable system disruption.

**Stealthy Execution:** Security tools are bypassed, delaying detection for days or weeks.

**Data Destruction:** Deletion of local and cloud backups to cripple recovery options.

---

Exfiltration and Double Extortion

**Data Exfiltration:** Sensitive files are copied to attacker-controlled servers before encryption.

**Leak Site Threats:** Stolen data is published on Conti’s dedicated leak site if ransoms are not paid.

**Negotiation Leverage:** Victims who share private negotiation chats risk immediate termination of talks and full data exposure. In some cases, Conti has threatened **“collective punishment”** — leaking another victim’s data if terms are violated.

![](image-2.png)

---

---

OPSEC Failure and Leaks

In 2022, following Conti’s declaration of support for Russia during the war in Ukraine, an insider leaked tens of thousands of chat logs and documents.

These **Conti leaks** revealed:

- Salaries, HR recruitment, and training sessions.
- Development discussions to improve malware.
- Demos of EDR products for bypass testing.
- Phishing templates for initial access.
- Screenshots of a **Conti control panel** with compromised hosts and telemetry.

The leaks exposed Conti as a **corporate-style ransomware enterprise** rather than a loose gang.

![](image-1024x480.png)

---

Conti operated much like a legitimate software company: leaked chats reveal active development discussions about new features for targeting victims and persistent challenges—such as reliably encrypting very large files. The group even sought demos of popular endpoint detection and response products, apparently to tailor their malware to evade detection.

Two operators, “**lemur**” and “**terry**,” shared phishing templates to weaponize against prospective victims — underscoring phishing’s role as a primary, cost-effective initial access vector for Conti. Phishing campaigns were frequently used to establish a foothold on target networks before follow-on tooling and lateral movement.

The leaks also included a screenshot of Conti’s control panel, which listed compromised hosts and provided detailed telemetry: operating system versions, installed antivirus products, user privilege levels, and other asset metadata — data that enabled the attackers to prioritize high-value targets and tailor their payloads.

![](image-1-1024x537.png)

---

Conti’s ransom note to the victims

```
All of your files are currently encrypted by CONTI strain. 

As you know (if you don't - just "google it"), all of the data that has been encrypted by our software cannot be recovered by any means without contacting our team directly. 
If you try to use any additional recovery software - the files might be damaged, so if you are willing to try - try it on the data of the lowest value.

To make sure that we REALLY CAN get your data back - we offer you to decrypt 2 random files completely free of charge.

You can contact our team directly for further instructions through our website :

TOR VERSION :
(you should download and install TOR browser first https://torproject.org)

http://contirec7nchr45rx6ympez5rjldibnqzh7lsa56lvjvaeywhvoj3wad.onion/

YOU SHOULD BE AWARE!
Just in case, if you try to ignore us. We've downloaded a pack of your internal data and are ready to publish it on out news website if you do not respond. So it will be better for both sides if you contact us as soon as possible.
```

![](image-3-1024x486.png)

---

Conti Members Profiles

1- Oleg Fakeev (aka White)

![](image-4-818x1024.png)

Source: [GangExposed](https://x.com/GangExposed_RU)

Among the revelations from the Conti leaks was the discovery of at least one active member attempting to mask his cybercriminal activities by claiming to operate a **cryptocurrency company**.

![](image-5.png)

GangExposed\_RU

---

2- Alexey Mikhailovich Kurashov (23.02.1986) has been identified as a key participant in the CONTI cybercriminal group, operating under the pseudonyms TARGET, BLOODRUSH, and RED

![](image-7.png)

source: GangExposed\_ERU

---

In addition to leaked chats and internal documents, open-source intelligence has revealed glimpses of Conti members showcasing the wealth generated from ransomware operations. In one notable case, a video released by **GangExposed** appeared to show **11 members of the Conti group on a yacht in Dubai, celebrating together**.

The footage portrays Conti not just as a cybercriminal collective but as a group of individuals enjoying the luxuries typically associated with successful entrepreneurs. Such displays highlight the **scale of financial rewards** ransomware syndicates can reap, and how those profits are often funneled into extravagant lifestyles far from the victims who suffer the consequences.

![](image-8.png)

---

Conti comprised well over 100 members, so introducing individuals in this blog would be impractical and counterproductive. Instead, we highlight the group’s behavior to show a stark contrast: while Conti systematically targeted critical sectors such as healthcare, dozens of its members openly enjoyed lavish lifestyles — yachts, luxury travel, and public celebrations — seemingly unconcerned by the real-world harm their operations caused. This disconnect underscores how modern ransomware syndicates can operate like profitable businesses, profiting from human suffering while maintaining pockets of normal, affluent life.

---

Conclusion

The story of **Conti ransomware** is more than just the rise and fall of a cybercriminal group — it is a case study in how modern **ransomware operations** mimic legitimate businesses. From double extortion tactics to corporate hierarchies, Conti industrialized cybercrime while inflicting harm on critical sectors.

Even though leaks and fractures disrupted Conti, its methods and infrastructure live on through spin-offs. The legacy continues to shape today’s ransomware landscape.

? For defenders, Conti is a reminder that combating ransomware requires not only technical defenses but also preparation, intelligence sharing, and organizational resilience.
