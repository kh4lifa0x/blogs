---
title: "Qilin Ransomware: A Deep Dive into Operations & OPSEC Breakdowns"
date: 2025-08-05 23:04:05 +0200
categories: [Ransomware]
tags: [investigation, opsec-failure, ransomware]
image:
  path: qilin.jpg
  alt: "Qilin Ransomware: A Deep Dive into Operations & OPSEC Breakdowns"
media_subpath: /assets/img/posts/qilin-ransomware-a-deep-dive-into-operations-opsec-breakdowns
toc: true
---

**A Major Power Shift: The Sudden Disappearance of RansomHub**  
  
One of the most pivotal developments in the ransomware landscape occurred in late March 2025, when **RansomHub**—widely regarded as the most prolific ransomware group of 2024—vanished without warning. Known for its highly professional **Ransomware-as-a-Service (RaaS)** operation, RansomHub had rapidly gained prominence by offering affiliates advanced cross-platform payloads (supporting **Windows, Linux, and ESXi**), timely profit sharing, and a reputation for transparent dealings.

Just as **RansomHub** appeared to be solidifying its dominance in the cybercrime ecosystem, its leak site abruptly disappeared. Within days, the rival threat group **DragonForce** publicly claimed to have absorbed RansomHub’s infrastructure and affiliate network, even incorporating the RansomHub logo into its own branding.

You can read our fully detailed blog about this major shift [here](https://darkatlas.io/blog/dragonforce-ransomware-from-hacktivism-to-global-cyber-extortion).

---

**Ransomware Affiliate**  
  
Recruitment of affiliates for the Qilin ransomware operation began surfacing on underground hacking forums in **late 2023**, marking the group’s transition into a **Ransomware-as-a-Service (RaaS)** model. Under this model, Qilin provides affiliates with comprehensive tooling and infrastructure to carry out attacks, while retaining **15–20%** of ransom payments as commission.

In **June 2024**, Qilin claimed responsibility for its most high-profile attack to date—**Synnovis**, a UK-based medical services provider supporting several London hospitals. The group reportedly demanded a **$50 million ransom** in exchange for withholding the release of **approximately 400GB of sensitive healthcare data**, highlighting Qilin’s growing sophistication and willingness to target critical sectors.

---

**Qilin Ransomware Hits Live on Social Media**  
  
**Qilin** is rapidly evolving beyond traditional ransomware operations, expanding its ecosystem with offerings such as legal and media support, petabyte-scale data storage, and spam delivery tools—positioning itself as a full-service cybercrime platform.

![](image-1.png)

---

**On July 31, 2025**, a post appeared on a dark web forum from affiliate member **“hastalamuerte,”** alleging that the **Qilin group had conducted an exit scam**, defrauding them of **$48,000**. This claim was later referenced on Twitter, adding to growing concerns about instability within the group’s affiliate program.  
  
Another user, operating under the handle **“Nova,”** publicly leaked the **Qilin affiliate panel**, including **login credentials**, further exposing the group’s operational security weaknesses.  
  
***NOVA*** is a newly emerged ransomware group rapidly gaining traction by launching affiliate panels and actively competing within the broader ransomware ecosystem. Such instances of **“internal exposure”** are common tactics used by rival groups to highlight and exploit the **OPSEC failures** of their competitors, undermining trust and attempting to poach affiliates.  
  
a message in **Russian** warning affiliates of the group’s compromised operations:

```
Их счета полны агентов ФБР и исследователей безопасности, и они используют свои собственные кошельки, поэтому вы должны понимать, что ваши деньги будут конфискованы, если вы внесете средства на их счета, особенно если это крупные суммы в миллионы долларов.

Защитник Windows быстро обслуживает все и сразу программы, так как она использует удобное программное обеспечение для сборки или, по крайней мере, для мобильных устройств, мере, другие комбинации.

Их система безопасности будет конфискована вместе со всеми деньгами в течение нескольких минут. Если правоохранительные органы будут сотрудничать, информация об используемом ними программном обеспечении для сборки вскоре будет раскрыта исследователями.

Считайте их мошеннической операцией будущего, и это один из ярких примеров.
```

**while translating this message** :

```
“Their accounts are full of FBI agents and security researchers, and they use their own wallets, so you should understand that your money will be confiscated if you deposit funds into their accounts, especially if it’s large amounts in the millions of dollars… Consider them a fraudulent operation of the future, and this is one of the clearest examples.”
```

![](image-2.png)
![](image-4-1024x302.png)

**Here is the Login Panel:**

![](image-3-1024x545.png)

---

Below is an image of the **Qilin ransomware affiliate panel**

![](image-5.png)

---

During the investigation into the affiliate **“hastalamuerte,”** several noteworthy indicators emerged—most notably, the frequent use of **Mimikatz**, a well-known credential dumping tool, suggesting its central role in the affiliate’s post-exploitation activities.

![](image-6.png)

---

The affiliate was observed creating and deploying a file named **“mim.exe,”** a renamed instance of **Mimikatz**, indicating efforts to evade basic detection while leveraging the tool for **credential harvesting** during post-exploitation.

![](image-7-1024x494.png)

---

**BITKUB – SPECIAL INTEREST IDENTIFIED**

During the investigation, a **Qilin affiliate** was observed interacting with **Bitkub**, one of **Thailand’s leading cryptocurrency exchanges**. Specifically, the affiliate utilized the official **Bitkub Python library**, which offers API access to key functionalities such as **trading, wallet/address creation, and fiat deposit/withdrawal** operations.

This finding suggests the threat actor may have **previous experience or an existing operational footprint involving Bitkub**, potentially using the exchange for laundering or facilitating ransom payments.

---

**NETEXECRU – The Russian Adaptation of NetExec**

On **May 7, 2025**, the threat actor uploaded a GitHub repository titled **“Шпаргалка по NetExec”**, which translates to **“NetExec Cheat Sheet”** in Russian. This appears to be a localized version of the popular post-exploitation tool **NetExec**, with all section headers and content written in **Russian**, indicating an intent to cater to **Russian-speaking operators** and streamline offensive operations within that community.

![](image-8.png)

---

![](image-9-1024x494.png)

---

---

An analysis of the GitHub activity associated with the affiliate **“hastalamuerte”** revealed several forked repositories of interest. Notably, one of the projects is **`php-mysql-dump`**, a lightweight script designed to **dump entire databases or tables into HTML format**, with support for column name output—potentially useful in data exfiltration or reconnaissance phases.

Additionally, there are signs of **interest in DeepSeek AI-related projects**, suggesting a possible exploration into **AI-enhanced capabilities or experimentation** with machine learning tools, although the intent behind this remains unclear.

![](image-10.png)

---

raises a GitHub issue on March 21 regarding proxy authentication in **sqlmap**, revealing use of proxy files containing plaintext credentials—highlighting both operational activity and poor OPSEC hygiene in handling sensitive data.

![](image-11.png)

---

The affiliate’s GitHub profile reveals starred topics that reflect dual interests in **financial exploitation** and **security evasion**—including areas like **algorithmic trading**, **arbitrage**, and **AV/antivirus evasion**—indicating a potential blend of cybercrime and fraud-related capabilities.

![](image-12.png)

---

---

“hastalamuerte,” showcasing recent activity and contributions to Kali Linux-related projects, with details like issue tracking and membership information.

![](image-13-1024x489.png)

---

The threat actor has shown repeated engagement with several high-profile **CVEs** on GitHub over time. While this does not confirm direct usage in **Qilin ransomware operations**, the observed activity suggests a **strong likelihood of experimentation or operational testing** involving these vulnerabilities:

- **CVE-2021-40444** – Microsoft MSHTML Remote Code Execution (0-day)
- **CVE-2022-30190** – *Follina* Remote Code Execution via Microsoft Support Diagnostic Tool
- **CVE-2023-36025** – Windows SmartScreen Security Feature Bypass
- **CVE-2024-30090** – Microsoft Streaming Service Elevation of Privilege
- **CVE-2025-53770** – SharePoint Toolshell Exploit *(new and potentially custom or private proof-of-concept)*

This interest in a diverse set of RCE, privilege escalation, and security bypass vulnerabilities aligns with **multi-stage intrusion workflows** observed in modern ransomware campaigns.

---

---

**Conclusion**

The rapid succession of events following the disappearance of RansomHub and the subsequent rise—and apparent turbulence—within Qilin’s operations underscore the dynamic volatility of today’s ransomware ecosystem. The absorption of RansomHub’s infrastructure by DragonForce signaled a major realignment of power, yet it also spotlighted just how fragile these illicit enterprises can be. The internal chaos and alleged exit scam within Qilin, amplified by leaks and public warnings from disgruntled affiliates like “hastalamuerte,” reveal deep fissures in trust and operational security among ransomware collectives, further compounded by active interference from law enforcement and rival groups.

Meanwhile, the technical behavior and open-source activity traced to key affiliates show an ongoing evolution in tradecraft—highlighting their adaptability, focus on financial manipulation, and shifting use of both established and novel attack tools. Interactions with cryptocurrency infrastructure and the embrace of emerging technologies like AI illustrate the increasingly sophisticated and multi-faceted approach adopted by contemporary threat actors.

Together, these developments highlight the high-stakes, rapidly shifting contest for dominance among ransomware groups, whose internal instability often matches the disruption they seek to inflict. For defenders, this means that vigilance, intelligence sharing, and constant adaptation remain vital in anticipating both the next group to rise—and the next to fall

---

---

Yara Rule

```
import "pe"

rule INDICATOR_EXE_Mimikatz_Generic
{
    meta:
        author = "AhmedKhalifa-DarkAtlas"
        description = "Detects executables containing Mimikatz artifacts (e.g., mim.exe)"

    strings:
        $name1 = "mimikatz" ascii nocase
        $name2 = "mim.exe" ascii nocase

    condition:
        uint16(0) == 0x5A4D and (
            $name1 or $name2 or
            for any i in (0 .. pe.number_of_sections - 1) :
                (
                    (pe.sections[i].name == ".text" or pe.sections[i].name == ".data") and
                    ($name1 or $name2)
                )
        )
}
```
