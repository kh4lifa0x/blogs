---
title: "Akira Ransomware Road To Glory"
date: 2025-04-14 23:52:14 +0200
categories: [Malware Analysis, Threat Intelligence]
tags: [malware-analysis]
image:
  path: WhatsApp-Image-2025-04-20-at-12.58.53-AM.jpeg
  alt: "Akira Ransomware Road To Glory"
media_subpath: /assets/img/posts/akira-ransomware-road-to-glory
toc: true
---

# Executive Summary

First Identified:  
**March 2023**

Operation Style:  
is a ransomware variant and ransomware deployment entity active since at least March 2023.**Akira**uses compromised credentials to access single-factor external access mechanisms such as VPNs for initial access, then various publicly-available tools and techniques for lateral movement. [Akira] operations are associated with “double extortion” ransomware activity, where data is exfiltrated from victim environments prior to encryption, with threats to publish files if a ransom is not paid. Technical analysis of **Akira** ransomware indicates multiple overlaps with and similarities to **conti** malware.

Extortion method:  
**Double Extortion** – combining the traditional ransomware extortion method (**encryption**) with exfiltration of victim’s sensitive data; the group threatens to leak the data via a data leak site if the ransom demand is not paid.

Most Frequently Targeted Industry:  
**Education**, **Finance**, **Manufacturing**, and **Healthcare**.

Most Frequently Targeted Victim HQ region:  
**North America**, **Europe**, and **Australia**.

![](2025-04-14_06-20.png)

Known Associations:  
**GOLD SAHARA**, **PUNK SPIDER**.

## Description

The **Akira** ransomware group has been active since March 2023, targeting diverse industries across **North America**, **the UK**, and **Australia**. Operating as a Ransomware-as-a-Service (RaaS) model, **Akira** employs a double-extortion strategy by stealing sensitive data before encrypting it. According to their leak site, the group claims to have compromised over **350** organizations.

From November **13** to **14**, the **Akira** ransomware group posted over **30** new victims on their data leak site, marking their highest single-day total since they began operations in March 2023. This milestone represents a record-breaking escalation in their activities and the volume of leaks shared in one day.

The **Akira** ransomware blog is organized into **five** sections. The “**Leaks**” section lists victims who refused to pay the ransom, leading the group to publicly release their encrypted data. The “**News**” section highlights new victims, likely organizations currently engaged in ransom negotiations.

In the ‘**Leaks**’ section we’ve seen **3** victims that already been published on the ‘**News**’ section, and **29** new ones. In the ‘News’ section, we’ve seen **3** new victims. Which basically means that **32** new victims were published in the group’s **DLS**, and three more refused to pay the ransom and were added to the ‘**Leaks**’ section.

Since **March 2023, Akira** ransomware has impacted a wide range of businesses and critical infrastructure entities in **North America**, **Europe**, and **Australia**. In **April 2023**, following an initial focus on Windows systems, **Akira** threat actors deployed a Linux variant targeting **VMware ESXi** virtual machines. As of **January 1, 2024**, the ransomware group has impacted over **250** organizations and claimed approximately **$42 million (USD)** in ransomware proceeds.

Early versions of the **Akira**ransomware variant were written in **C++** and encrypted files with a `.akira` extension; however, beginning in **August 2023**, some **Akira** attacks began deploying **Megazord**, using **Rust-based** code which encrypts files with a `.powerranges` extension.  **Akira** threat actors have continued to use both **Megazord** and **Akira**, including **Akira\_v2** (identified by trusted third party investigations) interchangeably.

The **FBI**, **CISA**, **EC3**, and **NCSC-NL** encourage organizations to implement the recommendations in the Mitigations section of this **CSA** to reduce the likelihood and impact of ransomware incidents.

![](2025-04-19_23-02.png)

## Previous Target: Akira

Of the **35** total posts, **25** originate from the **United States**. **Canada** accounts for two, while the remaining posts come from **Uruguay**, **Denmark**, **Germany**, **the United Kingdom**, **Sweden**, **the Czech Republic**, and **Nigeria**.

The Business Services sector is the most frequently targeted, with **10** organizations affected. Other impacted industries include **Manufacturing**, **Construction**, **Retail**, **Technology**, **Education**, and **Critical Infrastructure**.

From **November 13** to **14**, the Akira ransomware group posted over **30** new victims on their data leak site, marking their highest single-day total since they began operations in **March 2023**.

As of **January 1, 2024**, the ransomware group has impacted over **250** organizations and claimed approximately **$42 million (USD)** in ransomware proceeds.

![](2025-04-14_06-14.png)

## Data Leak Site: Akira

![](2025-04-14_06-13.png)

![](2025-04-14_06-13_1-1-1.png)

## Known Exploited CVEs

(**CVE-2023-20269**)

A vulnerability in the remote access VPN feature of Cisco Adaptive Security Appliance (ASA) Software and Cisco Firepower Threat Defense (FTD) Software could allow an unauthenticated, remote attacker to conduct a brute force attack in an attempt to identify valid username and password combinations or an authenticated, remote attacker to establish a clientless SSL VPN session with an unauthorized user. This vulnerability is due to improper separation of authentication, authorization, and accounting (AAA) between the remote access VPN feature and the HTTPS management and site-to-site VPN features.

(**CVE-2020-3259**)

A vulnerability in the web services interface of Cisco Adaptive Security Appliance **(ASA)** Software and Cisco Firepower Threat Defense **(FTD)** Software could allow an unauthenticated, remote attacker to retrieve memory contents on an affected device, which could lead to the disclosure of confidential information. The vulnerability is due to a buffer tracking issue when the software parses invalid URLs that are requested from the web services interface. An attacker could exploit this vulnerability by sending a crafted **GET** request to the web services interface. A successful exploit could allow the attacker to retrieve **memory** contents, which could lead to the disclosure of confidential information. Note: This vulnerability affects only specific AnyConnect and **WebVPN** configurations.

---

## Associations: Akira

**PUNK SPIDER**PUNK SPIDER is the Big Game Hunting **(BGH)** adversary (first identified in **April 2023**) responsible for developing and maintaining Akira ransomware and its associated **Akira** dedicated leak site **(DLS)**. Tactics, Techniques, and Procedures **(TTPs)** associated with Akira ransomware deployments include significant use of legitimate repurposed software and **Open-Source** penetration-testing tools.

**GOLD SAHARA**GOLD SAHARA is a cybercrime group that deploys **Akira** ransomware. The first **Akira** victim was named on a dedicated leak site in **April 2023**. There is no evidence that **Akira** is operated as ransomware-as-a-service **(RaaS)**, but the rate of naming victims on the **Akira** leak site, at around **30** a month, suggests a large group of individuals is responsible for **Ransomware** deployment.

**GOLD SAHARA** exclusively uses off-the-shelf tools and built-in utilities to conduct its operations. After compromising **VPN** accounts for **initial access**, the group uses **Advanced IP Scanner** and the **SoftPerfect** Network Scanner for network discovery, and the built-in **Nltest** Windows utility to identify **Domain** trusts and domain controllers. It uses **AnyDesk** and **PuTTy** for remote access, and the **WinRAR** archiving tool to stage data for exfiltration using **Rclone**. The group has also been observed accessing and downloading **SharePoint** files to use in extortion attempts. Prior to deploying ransomware, **GOLD SAHARA** deletes **Administrator Accounts**, likely to hinder recovery efforts.

## Known Tools: Akira

**indicates behaviors that have been observed by DarkAtlas Team.**

**Malicious Files Affiliated with Akira Ransomware:**

| **File Name** | **Hash (SHA-256)** | **Description** |
| --- | --- | --- |
| **w.exe** | d2fd0654710c27dcf37b6c1437880020824e161dd0bf28e3a133ed777242a0ca | Akira ransomware |
| **Win.exe** | dcfa2800754e5722acf94987bb03e814edcb9acebda37df6da1987bf48e5b05e | Akira ransomware encryptor |
| **AnyDesk.exe** | bc747e3bf7b6e02c09f3d18bdd0e64eef62b940b2f16c9c72e647eec85cf0138 | Remote desktop application |
| **Gcapi.dll** | 73170761d6776c0debacfbbc61b6988cb8270a20174bf5c049768a264bb8ffaf | DLL file that assists with the execution of AnyDesk.exe |
| **Sysmon.exe** | 1b60097bf1ccb15a952e5bcc3522cf5c162da68c381a76abc2d5985659e4d386 | Ngrok tool for persistence |
| **Config.yml** | Varies by use | Ngrok configuration file |
| **Rclone.exe** | aaa647327ba5b855bedea8e889b3fafdc05a6ca75d1cfd98869432006d6fecc9 | Exfiltration tool |
| **Winscp.rnd** | 7d6959bb7a9482e1caa83b16ee01103d982d47c70c72fdd03708e2b7f4c552c4 | Network file transfer program |
| **WinSCP-6.1.2-Setup.exe** | 36cc31f0ab65b745f25c7e785df9e72d1c8919d35a1d7bd4ce8050c8c068b13c | Network file transfer program |
| **Akira\_v2** | 3298d203c2acb68c474e5fdad8379181890b4403d6491c523c13730129be3f75 0ee1d284ed663073872012c7bde7fac5ca1121403f1a5d2d5411317df282796c | Akira\_v2 ransomware |
| **Megazord** | ffd9f58e5fe8502249c67cad0123ceeeaa6e9f69b4ec9f9e21511809849eb8fc dfe6fddc67bdc93b9947430b966da2877fda094edf3e21e6f0ba98a84bc53198 131da83b521f610819141d5c740313ce46578374abb22ef504a7593955a65f07 9f393516edf6b8e011df6ee991758480c5b99a0efbfd68347786061f0e04426c 9585af44c3ff8fd921c713680b0c2b3bbc9d56add848ed62164f7c9b9f23d065 2f629395fdfa11e713ea8bf11d40f6f240acf2f5fcf9a2ac50b6f7fbc7521c83 7f731cc11f8e4d249142e99a44b9da7a48505ce32c4ee4881041beeddb3760be 95477703e789e6182096a09bc98853e0a70b680a4f19fa2bf86cbb9280e8ec5a 0c0e0f9b09b80d87ebc88e2870907b6cacb4cd7703584baf8f2be1fd9438696d C9c94ac5e1991a7db42c7973e328fceeb6f163d9f644031bdfd4123c7b3898b0 | Akira “Megazord” ransomware |
| **VeeamHax.exe** | aaa6041912a6ba3cf167ecdb90a434a62feaf08639c59705847706b9f492015d | Plaintext credential leaking tool |
| **Veeam-Get-Creds.ps1** | 18051333e658c4816ff3576a2e9d97fe2a1196ac0ea5ed9ba386c46defafdb88 | PowerShell script for obtaining and decrypting accounts from Veeam servers |
| **PowershellKerberos TicketDumper** | 5e1e3bf6999126ae4aa52146280fdb913912632e8bac4f54e98c58821a307d32 | Kerberos ticket dumping tool from LSA cache |
| **sshd.exe** | 8317ff6416af8ab6eb35df3529689671a700fdb61a5e6436f4d6ea8ee002d694 | OpenSSH Backdoor |
| **ipscan-3.9.1-setup.exe** | 892405573aa34dfc49b37e4c35b655543e88ec1c5e8ffb27ab8d1bbf90fc6ae0 | Network scanner that scans IP addresses and ports |

## Observed Akira Behaviors: Windows

#### **Initial Access**

The **FBI** and cybersecurity researchers have observed **Akira** threat actors obtaining initial access to organizations through a virtual private network **(VPN)** service without multifactor authentication **(MFA)** configured, mostly using known **Cisco** vulnerabilities Additional methods of initial access include the use of external-facing services such as **Remote Desktop Protocol (RDP)** , spear phishing **Phishing,Spearphishing** and the abuse of valid credentials.

#### **Persistence and Discovery**

Once initial access is obtained, **Akira** threat actors attempt to abuse the functions of domain controllers by creating new domain accounts to establish persistence. In some instances, the **FBI** identified Akira threat actors creating an **Administrative Account** named `itadm`.

According to **FBI** and open source reporting, **Akira** threat actors leverage post-exploitation attack techniques, such as **Kerberoasting** to extract **Credentials** stored in the process memory of the Local Security Authority Subsystem Service **(LSASS)**. Akira threat actors also use credential scraping tools like **Mimikatz** and **LaZagne**to aid in privilege escalation. Tools like **SoftPerfect** and **Advanced IP Scanner** are often used for network device discovery **(reconnaissance)** purposes and `net` Windows commands are used to identify domain controllers and gather information on domain trust relationships

#### **Defense Evasion**

Based on trusted third party investigations, **Akira** threat actors have been observed deploying **two** distinct ransomware variants against different system architectures within the same compromise event. This marks a shift from recently reported **Akira** ransomware activity. **Akira** threat actors were first observed deploying the Windows-specific “**Megazord**” ransomware, with further analysis revealing that a second payload was concurrently deployed in this attack (which was later identified as a novel variant of the **Akira** **ESXi encryptor**, “**Akira\_v2**”).

As **Akira** threat actors prepare for lateral movement, they commonly disable security software to avoid detection. Cybersecurity researchers have observed **Akira** threat actors using **PowerTool** to exploit the **Zemana AntiMalware** driver

#### **Exfiltration and Impact**

**Akira** threat actors leverage tools such as **FileZilla**, **WinRAR** , **WinSCP**, and **RClone** to exfiltrate data To establish command and control channels, threat actors leverage readily available tools like **AnyDesk**, **MobaXterm**, **RustDesk**, **Ngrok**, and **Cloudflare Tunnel**. Enabling exfiltration through various protocols such as File Transfer Protocol **(FTP)**, Secure File Transfer Protocol **(SFTP)**, and cloud storage services like **Mega** to connect to exfiltration servers.

**Akira** threat actors use a double-extortion model after exfiltrating data. The **Akira** ransom note provides each company with a **unique code** and instructions to contact the threat actors via `.onion` URL. **Akira** threat actors do not leave an initial ransom demand or payment instructions on compromised networks, and do not relay this information until contacted by the **victim**. Ransom payments are paid in **Bitcoin** to cryptocurrency wallet addresses provided by the threat actors. To further apply pressure, **Akira** threat actors threaten to publish exfiltrated data on the Tor network, and in some instances have called **Victimized** companies, according to **FBI** reporting.

#### **Encryption**

**Akira** threat actors utilize a **sophisticated hybrid encryption** scheme to lock data. This involves combining a **ChaCha20** stream cipher with an **RSA** public-key cryptosystem for speed and secure key exchange . This multilayered approach tailors encryption methods based on **file type** and **size** and is capable of full or partial encryption. Encrypted files are appended with either a `.akira` or `.powerranges` extension. To further inhibit system recovery, Akira’s encryptor (`w.exe`) utilizes PowerShell commands to delete volume shadow copies **(VSS)** on Windows systems . Additionally, a ransom note named `fn.txt` appears in both the root directory (`C:`) and each users’ home directory (`C:\Users`).

Trusted third party analysis identified that the **Akira\_v2** encryptor is an upgrade from its previous version, which includes additional functionalities due to the language it’s written in **(Rust)**. Previous versions of the encryptor provided options to insert arguments at runtime, including:

- `-p --encryption_path (targeted file/folder paths)`
- `-s --share_file (targeted network drive path)`
- `-n --encryption_percent (percentage of encryption)`
- `--fork (create a child process for encryption`

The ability to insert additional threads allows **Akira** threat actors to have more granular control over the number of **CPU** cores in use, increasing the speed and efficiency of the encryption process. The new version also adds a layer of protection, utilizing the **Build ID** as a run condition to hinder dynamic analysis. The **encryptor** is unable to execute successfully without the unique Build ID. The ability to deploy against only virtual machines using “`vmonly`” and the ability to stop running virtual machines with “`stopvm`” functionalities have also been observed implemented for **Akira\_v2**. After encryption, the Linux ESXi variant may include the file extension “`akiranew`” or add a ransom note named “`akiranew.txt`” in directories where files were encrypted with the new nomenclature.

## MITRE ATT&CK® Mappings: Akira

### Techniques Used

#### **Table 1: Initial Access**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Valid Accounts | T1078 | Akira threat actors obtain and abuse credentials of existing accounts as a means of gaining initial access. |
| Exploit Public Facing Application | T1190 | Akira threat actors exploit vulnerabilities in internet-facing systems to gain access to systems. |
| External Remote Services | T1133 | Akira threat actors have used remote access services, such as RDP/VPN connection to gain initial access. |
| Phishing: Spearphishing Attachment | T1566.001 | Akira threat actors use phishing emails with malicious attachments to gain access to networks. |
| Phishing: Spearphishing Link | T1566.002 | Akira threat actors use phishing emails with malicious links to gain access to networks. |

#### **Table 2: Credential Access**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| OS Credential Dumping | T1003 | Akira threat actors use tools like Mimikatz and LaZagne to dump credentials. |
| OS Credential Dumping: LSASS Memory | T1003.001 | Akira threat actors attempt to access credential material stored in the process memory of the LSASS. |

#### **Table 3: Discovery**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| System Network Configuration Discovery | T1016 | Akira threat actors use tools to scan systems and identify services running on remote hosts and local network infrastructure. |
| System Information Discovery | T1082 | Akira threat actors use tools like PCHunter64 to acquire detailed process and system information. |
| Domain Trust Discovery | T1482 | Akira threat actors use the net Windows command to enumerate domain information. |
| Process Discovery | T1057 | Akira threat actors use the Tasklist utility to obtain details on running processes via PowerShell. |
| Permission Groups Discovery: Local Groups | T1069.001 | Akira threat actors use the net localgroup /dom to find local system groups and permission settings. |
| Permission Groups Discovery: Domain Groups | T1069.002 | Akira threat actors use the net group /domain command to attempt to find domain level groups and permission settings. |
| Remote System Discovery | T1018 | Akira threat actors use nltest /dclist to amass a listing of other systems by IP address, hostname, or other logical identifiers on a network. |

#### **Table 4: Persistence**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Create Account: Domain Account | T1136.002 | Akira threat actors attempt to abuse the functions of domain controllers by creating new domain accounts to establish persistence. |

#### **Table 5: Defense Evasion**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Impair Defenses: Disable or Modify Tools | T1562.001 | Akira threat actors use BYOVD attacks to disable antivirus software. |

#### **Table 6: Command and Control**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Remote Access Software | T1219 | Akira threat actors use legitimate desktop support software like AnyDesk to obtain remote access to victim systems. |
| Proxy | T1090 | Akira threat actors utilized Ngrok to create a secure tunnel to servers that aided in exfiltration of data. |

#### **Table 7: Collection**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Archive Collected Data: Archive via Utility | T1560.001 | Akira threat actors use tools like WinRAR to compress files. |

---

#### **Table 8: Exfiltration**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Exfiltration Over Alternative Protocol | T1048 | Akira threat actors use file transfer tools like WinSCP to transfer data. |
| Transfer Data to Cloud Account | T1537 | Akira threat actors use tools like CloudZilla to exfiltrate data to a cloud account and connect to exfiltration servers they control. |
| Exfiltration Over Web Service: Exfiltration to Cloud Storage | T1567.002 | Akira threat actors leveraged RClone to sync files with cloud storage services to exfiltrate data. |

---

#### **Table 9: Impact**

| **Technique Title** | **ID** | **Use** |
| --- | --- | --- |
| Data Encrypted for Impact | T1486 | Akira threat actors encrypt data on target systems to interrupt availability to system and network resources. |
| Inhibit System Recovery | T1490 | Akira threat actors delete volume shadow copies on Windows systems. |
| Financial Theft | T1657 | Akira threat actors use a double-extortion model for financial gain. |

## Conclusion

The **Akira** ransomware group has emerged as a formidable threat since its first appearance in **March 2023,** targeting over **250** organizations and amassing approximately **$42 million** in ransomware proceeds. Operating under a double-extortion model, **Akira** combines data encryption with the exfiltration of sensitive information, pressuring victims to pay by threatening public exposure. The group’s tactics involve leveraging compromised **VPN** credentials and known vulnerabilities in **Cisco** products to gain initial access, followed by network reconnaissance, privilege escalation, and data exfiltration using widely available tools such as **AnyDesk**, **RClone** and **WinSCP**.

The ransomware has evolved over time, initially written in **C++** and later incorporating **Rust**-based code in the **Megazord** variant. This shift reflects the group’s commitment to enhancing encryption speed and resilience against detection. The targeting of diverse industries, including **business services**, **Manufacturing**, **Technology**, and **critical infrastructure**, highlights the widespread and indiscriminate nature of **Akira’s** operations.

To mitigate the threat posed by **Akira** ransomware, organizations are urged to strengthen their cybersecurity posture by implementing multi-factor authentication **(MFA)**, securing **VPN** access, and maintaining regular **data backups**. **The Akira** group’s rapid adaptation to defensive measures underscores the need for continuous monitoring and proactive threat intelligence to stay ahead of this evolving threat landscape.
