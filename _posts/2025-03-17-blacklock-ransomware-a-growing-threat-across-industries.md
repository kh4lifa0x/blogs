---
title: "BlackLock Ransomware: A Growing Threat Across Industries"
date: 2025-03-17 00:11:11 +0200
categories: [Malware Analysis, Threat Intelligence]
tags: [malware-analysis, threat-actors]
image:
  path: blacklock.jpeg
  alt: "BlackLock Ransomware: A Growing Threat Across Industries"
media_subpath: /assets/img/posts/blacklock-ransomware-a-growing-threat-across-industries
toc: true
---

**BlackLock** could become the most active **RaaS** group of 2025.

The latest threat report from the **[DarkAtlas](https://darkatlas.io/) Research Team**, titled *“**Inside the World’s Fastest Rising Ransomware Operator —* ***BlackLock****”* underscores its critical relevance across the industry due to the group’s unpredictable tactics and lack of operational patterns. The report provides a detailed analysis of the rapid rise of ***BlackLock*** (also known as *El Dorado*) in 2024, highlighting how it has swiftly positioned itself as a major ransomware threat. It also includes strategic, actionable recommendations to help organizations mitigate the risks associated with this emerging threat.

***BlackLock*** has emerged as one of the most notorious ransomware groups in 2025, gaining widespread infamy for publicly listing numerous high-profile victims on their leak site. Their rapid rise and sophisticated attack methods have positioned them as a major threat in the cybersecurity landscape, underscoring the urgent need for enhanced defensive strategies and proactive threat mitigation.

![](1_Ck33gf7DK_p7lIgyRW1aBg.png)

Impact of **BlackLock** Ransomware on Various Sectors in 2025 — The Miscellaneous and Technology sectors were hit hardest, underscoring the urgent need for robust cybersecurity strategies to mitigate future threats.

![](1_D5iYxzDPaqiRTVcHOEaMew.png)

BlackLock renames encrypted files with a random character string and appends them with a likewise randomized extension.

After the encryption process is completed, a ransom note titled “**HOW\_RETURN\_YOUR\_DATA.TXT**” is created.

![](1_OkuT4vswVJkPCDEBh0hP_w.png)

The first two months of the year have seen **BlackLock** ransomware execute **48 attacks** on organizations across various sectors, according to research by the [**DarkAtlas**](https://darkatlas.io/) **Research Team**. Construction and real estate firms have emerged as some of the most frequently targeted industries, highlighting a strategic shift in BlackLock’s attack patterns.

“The growing sophistication of ransomware operations like ***BlackLock***, coupled with the rise of Ransomware-as-a-Service (RaaS) platforms, has made it easier for threat actors to scale their operations rapidly,” the DarkAtlas Research Team reports. “This surge reflects a growing trend where cybercriminals are increasingly focusing on industries with high-value assets and complex operational structures.”

Some of the attacks in the sector also reflect the alignment of geopolitical and cybercriminal interests, according to the **DarkAtlas Research Team**. “Hacktivist groups, influenced by the current geopolitical climate, are increasingly leveraging ransomware — particularly **BlackLock** — in their operations, targeting critical industries such as **Construction** and **Technology** to maximize disruption and financial gain,” the team noted.

That’s not to say that other sectors are immune. According to the **DarkAtlas Research Team**, **IT service** providers have also been prime targets for BlackLock ransomware, as a single breach can enable the group to compromise downstream business customers. Additionally, nearly a quarter of the attacks have targeted government agencies, with threat actors employing both ransomware and more destructive wipers to maximize disruption and leverage.

![](1_KCVvC_enG71h6EAUbED-kg.png)

Telegram account linked to **BlackLock** ransomware, identified as “**Mamona R.I.P**,” highlighting the group’s presence on encrypted messaging platforms for coordination and communication.

## History and Evolution of BlackLock

Recent intelligence gathered by the **DarkAtlas** Research Squad indicates that **BlackLock** is, in fact, a rebranded version of the notorious **Eldorado** ransomware group. After facing increased scrutiny and pressure from law enforcement and cybersecurity researchers, the Eldorado operators have resurfaced under the BlackLock banner with a refined operational model and enhanced capabilities. This strategic rebranding follows a common pattern among ransomware groups — similar to the transitions from **Babuk** to **BabLock** and **REvil** to **BlackMatter** — where threat actors aim to evade detection, disrupt attribution efforts, and recruit new affiliates under a fresh identity. BlackLock retains the technical foundation of Eldorado’s malware, including its use of **Golang** for cross-platform attacks and its sophisticated encryption mechanisms (**ChaCha20** and **RSA-OAEP**), but has introduced more targeted attack strategies and faster encryption speeds to increase pressure on victims. This continuity in tactics and infrastructure strongly suggests that BlackLock is not an entirely new player but a strategic evolution of Eldorado, positioning itself as a dominant force in the RaaS ecosystem.

In **March 2024**, a new affiliate program linked to the ransomware group **Eldorado** was advertised on the underground forum **“RAMP.”** The post promoted both a ransomware locker and loader, while actively recruiting penetration testers to support the group’s growing operations. The **DarkAtlas** Research Squad has been monitoring Eldorado closely and has uncovered significant details about the group’s structure, methods, and technical capabilities.

Our analysts infiltrated Eldorado’s network and determined that the group’s representative is a **Russian speaker**. The ransomware builder provided to affiliates requires elevated network access — including the **domain administrator’s password** or **NTLM (New Technology LAN Manager) hash** — to create tailored ransomware samples designed to maximize damage and increase the likelihood of payment.

**The Eldorado** has two versions of the malware in its arsenal – for Windows and Linux. However, this development is unique and does not rely on previously published builder sources. For example, on September 21, 2022, the builder for LockBit 3.0 ransomware was leaked, allowing various threat actors to create their own versions and conduct numerous high-profile attacks using its robust encryption and evasion techniques. Similarly, the Babuk ransomware source code was leaked on September 1, 2021, leading to the creation of multiple ransomware strains by different groups to exploit and exfiltrate data from targeted networks. Notable examples include the LIMPOPO (aka **SOCOTRA**, **FORMOSA**, **SEXi**) ransomware group, .

BlackLock actively recruits key players, known as traffers, to support the early stages of ransomware attacks. These individuals drive malicious traffic, steer victims to harmful content, and help establish initial access for campaigns. Recruitment posts for traffers explicitly outline requirements, signaling BlackLock’s urgency to bring on candidates quickly — often prioritizing speed over operational security.

In contrast, posts seeking higher-level developer and programmer roles are far more discreet, with details and resumes shared privately instead. These roles likely involve greater trust, higher compensation, and long-term commitment, making the recruitment process more delicate.

**El Dorado**’s ransomware employs advanced encryption techniques, utilizing the Go programming language for cross-platform compatibility. It employs **Chacha20** for file encryption and **RSA-OAEP** for key encryption, allowing it to encrypt files on shared networks using the Server Message Block (SMB) protocol.

 **El Dorado** targeted Acumen Group, an IT services company specializing in Enterprise Resource Planning (ERP) solutions. The attack disrupted operations, encrypting critical data and demanding a ransom for its release.  
   
the group identified is actively recruiting **traffers** who possess a complete set of their own tools. The group promises to cover any associated expenses and offers a profit-sharing arrangement as part of the deal. The post concludes with a direct statement of intent: **“The primary objective, of course, is to gain access to networks and secure ransom payments.”**

![](1_gQWTyWrT5IaVfViiYcFX4w.png)

## Advanced and Independent Development

Eldorado maintains a distinct edge over other ransomware operators by developing its own malware rather than relying on leaked builder sources. The group has crafted two separate ransomware versions — one for **Windows** and one for **Linux** — allowing them to execute attacks across different operating systems with high efficiency.

This independent development approach sets Eldorado apart from previous ransomware groups that have capitalized on leaked source code:

- **LockBit 3.0:** The builder was leaked in **September 2022**, enabling other threat actors to launch customized versions that triggered a spike in high-impact attacks.
- **Babuk:** The Babuk ransomware builder was leaked in **September 2021**, which gave rise to spin-offs like **LIMPOPO (SOCOTRA, FORMOSA, SEXi)** ransomware, **BabLock**, and **Estate** ransomware.

## Why BlackLock Matters — And How to Defend Against It

**BlackLock**’s rise as a major RaaS (Ransomware-as-a-Service) operator underscores a broader shift in the ransomware landscape — and it’s one that organizations can’t afford to ignore. The group’s success in targeting a wide range of industries, including construction, real estate, and government agencies, reflects both the growing sophistication of ransomware operations and the increased vulnerability of complex business networks.

So why does this matter? Because **BlackLock**’s methods — fast encryption, targeted attacks, and strategic use of leak sites — are becoming the blueprint for modern ransomware campaigns. Even if **BlackLock** itself eventually dissolves or rebrands, the tactics and infrastructure it established will likely persist, influencing future threat actors. Affiliates and spin-offs could emerge, bringing the same operational efficiency and aggressive targeting strategies to new ransomware variants.

Understanding **BlackLock**’s tactics is critical for building a resilient defense strategy. The rise of RaaS platforms has made it easier than ever for threat actors to scale their operations, lowering the barrier to entry and increasing the volume of attacks. Organizations that fail to adapt to this evolving threat landscape risk becoming easy targets.

That’s where the [**DarkAtlas**](https://darkatlas.io/) **Squad** can help. Our team specializes in ransomware mitigation and recovery, offering tailored solutions to strengthen your organization’s defenses against evolving threats like **BlackLock**. From advanced threat detection and incident response to secure data recovery and strategic advisory services, DarkAtlas provides the expertise needed to minimize risk and respond effectively when an attack occurs. Don’t wait for the next wave of ransomware — take action now to protect your business.
