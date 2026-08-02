---
title: "MuddyWater: Inside Iran’s Persistent Cyber-Espionage Group Targeting the Middle East"
date: 2025-08-24 22:29:46 +0200
categories: [Threat Intelligence]
tags: [investigation, threat-actors]
image:
  path: muddy.jpg
  alt: "MuddyWater: Inside Iran’s Persistent Cyber-Espionage Group Targeting the Middle East"
media_subpath: /assets/img/posts/muddywater-inside-irans-persistent-cyber-espionage-group-targeting-the-middle-east
toc: true
---

**MuddyWater**, a long-running **Iranian cyber-espionage** group **affiliated with Iran’s Ministry of Intelligence and Security (MOIS)**, has established itself as one of the most persistent state-backed threats on the global stage. Active since at least **2017**, the group has built a reputation for blending **off-the-shelf tools with custom malware** to achieve its goals. Over the past year, **MuddyWater** has intensified its activity, spearheading **phishing campaigns across the Middle East** — with Israel emerging as a primary target.

Since October 2023, these operations have **ramped up in both frequency and sophistication**, signaling a heightened strategic push. True to their modus operandi, the attackers rely heavily on **emails sent from compromised accounts**, exploiting trust within organizations and across supply chains. These phishing campaigns often pave the way for the installation of **commercial Remote Management Tools (RMMs)** such as Atera Agent or **ScreenConnect** — legitimate software twisted into tools of persistence and surveillance.

What makes their recent activity more alarming is the introduction of a **new custom backdoor, “BugSleep,”** designed to provide discreet and long-lasting access to compromised systems. Alongside **BugSleep**, investigators have observed **MuddyWater** **abusing legitimate platforms like Egnyte** — a trusted file-sharing service — as part of their command-and-control infrastructure. This blend of “living-off-the-land” tactics with bespoke malware underscores the group’s ability to adapt and evolve its toolbox while remaining difficult to detect.

---

**Targeted Sectors**

**MuddyWater’s** campaigns are marked by the mass distribution of phishing emails from compromised accounts, often targeting hundreds of recipients across more than 10 sectors. While their lures span a wide range of organizations and individuals, the group routinely zeroes in on specific industries or sectors, revealing their strategic interests. Most notably, recent campaigns have targeted **Israeli** municipalities, **airlines, travel agencies, and journalists**. These phishing efforts ramped up dramatically from **February 2024,** with researchers identifying over 50 spear phishing emails linked to **MuddyWater’s** operations.

Within each campaign, **MuddyWater** customizes its phishing lures for specific targets — such as encouraging municipal employees to download a supposed new app. This tactic, coupled with their broad targeting and volume, reflects the group’s persistent efforts to infiltrate sensitive networks and influence key industries in Israel and beyond.

![](0_xIEw7Al4T2-6oUoW.png)

---

****Attack Chain****

**MuddyWater** attacks unfold through a calculated, multi-stage process that leverages both social engineering and technical skill to compromise targets:

- **Initial Access:** The group is notorious for its use of spear-phishing campaigns, often sending seemingly legitimate emails from compromised accounts to a wide range of targets. These emails typically contain malicious attachments or links hosted on trusted file-sharing services, enticing users to open weaponized documents.
- **Payload Deployment**: Upon successful engagement, **MuddyWater** rapidly shifts to establishing persistent access — often by deploying legitimate Remote Monitoring and Management (RMM) tools like Atera Agent, ScreenConnect, Remote Utilities, and eHorus. This misuse of commercial software enables attackers to sidestep detection and blend in with normal network activity.
- **Privilege Escalation & Lateral Movement:** Once a foothold is established, MuddyWater actors use credential-dumping utilities such as Mimikatz to harvest credentials, aiming for local administrator access. They also deploy PowerShell scripts and web shells to broaden their compromise and maintain persistence.
- **Command & Control (C2):** Communication with C2 servers commonly occurs over DNS tunneling or through obfuscated data channels. MuddyWater utilizes tools like vpnui[.]exe (a unique Ligolo fork) and leverages protocols familiar to defenders, making detection challenging.
- **Malware and Backdoors:** Recently, the group has been seen delivering custom malware like BugSleep to maintain deep and long-term access, adapting payloads for different environments and sectors.
- **Evasion Techniques:** Their arsenal includes DLL side-loading, masquerading, and heavy use of obfuscated scripts to evade security controls and sandboxing.

![](0_56HzXZ31l6WQG_ly.png)

---

### **MuddyWater’s toolkit:**

- **PowGoop DLL Loader**: This malware acts as a loader, masquerading as a legitimate Google Update executable to evade detection. It is used to execute additional malicious payloads, hiding its communications with command-and-control (C2) servers under the guise of trusted software.
- **Small Sieve:** A Telegram Bot API-based Python backdoor distributed via a Nullsoft Scriptable Install System (NSIS) installer, typically named gram\_app.exe. Once installed, it achieves persistence by adding a registry run key and leverages custom obfuscation to avoid detection. Communication and tasking are performed via the Telegram API over HTTPS, with data further obfuscated using a hex byte swapping technique and an encoded Base64 function.
- **Canopy (Starwhale):** A spyware module that collects basic system information such as username, computer name, and IP address, and sends it to **MuddyWater-controlled** infrastructure for reconnaissance and targeting.
- **Mori:** A backdoor exploiting DNS tunneling to covertly communicate with MuddyWater’s C2 servers. This approach makes network monitoring and detection particularly challenging.
- **POWERSTATS:** A powerful backdoor that runs obfuscated PowerShell scripts, enabling persistent access and further command execution on compromised systems, broadening the attacker’s capabilities while minimizing detection.
- **BugSleep:** A custom backdoor engineered to execute commands on demand and facilitate file transfers between an infected machine and MuddyWater’s C2 servers. Still under active development, **BugSleep** is continuously being enhanced and improved by the group.

---

In the fall of 2022, uncovered the IP address **51.254.25[.]36** as part of **MuddyWater’s** infrastructure — showing activity linked to this APT group going back to at least **February 2022**. Further analysis tied this IP to a suspicious executable named new aviation communications.exe, which is characteristic of **MuddyWater’s** tactic of deploying disguised payloads to target the aviation and communications sectors. This finding highlights the group’s ability to leverage custom malware linked to specific operational goals and underscores their ongoing focus on infrastructure and lateral movement in targeted intrusions.

![](0_oTRdjr01kkxUiFfm.png)

---

**SimpleHelp** by SimpleHelp Ltd (UK) is an administration panel for system administrators and tech support teams. It looks like this:

![](0_2FqFWlp-g9nOzmQN.png)

---

---

### Atera Agent

**MuddyWater** has recently intensified the use of Atera Agent, a legitimate Remote Monitoring and Management (RMM) tool, as part of its aggressive attack campaigns. Since late 2023, the group has refined its phishing tactics, distributing spear-phishing emails that carry malicious RAR archives. These RAR files are encrypted to evade detection by security software, forcing recipients to engage step-by-step with email content and download instructions that lead ultimately to the execution of the RMM tools.

![](0_wWsJ-jaP4Kn3qQxY.png)

---

MuddyWater’s recent campaigns using Atera Agent typically involve sending a compressed RAR file named digitalform.rar as an email attachment, which is decrypted using the password **“123456”**. Inside this archive is an **MSI** installation package for the Atera Agent remote monitoring tool.

During installation, the Atera Agent uses a built-in system account and a corresponding unique ID to connect directly to the Atera control console. This allows attackers to remotely control the infected system through Atera’s legitimate platform without setting up their own infrastructure. The installation process is silent and does not require user interaction beyond executing the MSI file extracted from the RAR archive.

![](0_smFge14TEr29ttng.png)

---

Once installed, the attacker gains full remote control over the victim’s computer through the **Atera** Agent platform. This control enables a broad range of actions including:

- Executing arbitrary commands remotely on the compromised system.
- Downloading and uploading files to and from the infected machine.
- Monitoring system activity in real time.
- Running additional third-party remote monitoring and management (RMM) software such as **Splashtop**, **AnyDesk**, **TeamViewer**, and **ScreenConnect** to maintain flexible and redundant remote access.

![](0_bSQexXSbnZ6RZRQJ.png)

---

It should be noted that a recent MuddyWater campaign involved distributing an Atera Agent installation package through the trusted file-sharing platform **Egnyte**, using a subdomain disguised to resemble a university in a Middle Eastern country (**kinnneretacil.egnyte[.]com**). The attackers crafted spear-phishing emails with links pointing to this Egnyte-hosted resource, which contained a ZIP archive holding the malicious Atera Agent installer.

![](0_kHbFzhWih-2Nmfq1.png)

---

### ScreenConnect

MuddyWater’s phishing campaigns have employed a layered social engineering approach, using decoy documents to lure victims deeper into infection. In one notable campaign, the attackers induced users to progress layer by layer through email content, which ultimately led to the installation of the **ScreenConnect** remote monitoring software on the victim’s system.

![](0_5zurQRNsbXDoFLxI.png)

---

In a recent MuddyWater phishing campaign, the decoy document contained a counterfeit hyperlink that led victims to the legitimate cloud storage service OneHub at the URL:  
ws.onehub.com/files/7w1372el.

This link downloaded a ZIP file named “**المنحالدراسیة.zip”** (which translates to “**scholarship.zip**”) with the MD5 hash **960594cbdf938bcb03bd0637843d9154**. Inside the ZIP archive was an executable file with the same name, which, when run, installed the legitimate **ScreenConnect** remote access software.

This delivery mechanism allowed **MuddyWater** to disguise its malicious activity under the veil of a seemingly benign and contextually relevant file — a scholarship announcement likely appealing to targets in the region. Upon execution, the **ScreenConnect** tool provided the threat actors remote control over the compromised system, enabling persistent espionage operations.

![](0_V1v0B9veBIXuRz36.png)

---

After the installation completes, the **ScreenConnect** Client service is created and automatically launched on the victim’s system. This service runs stealthily in the background, making it difficult for users to detect its presence through normal system use or casual inspection.

![](0_QDNTbzgT1j8N_j-S.png)

---

The ScreenConnect Client service startup parameters include critical connection details that enable the client to actively connect to the control terminal (C2 server). These parameters typically encode information such as:

- Session type (e.g., Access)
- Client type or role (e.g., Guest)
- Server URL or instance hostname (e.g., instance-sy9at2-relay.screenconnect.com)
- Port (e.g., 443 for HTTPS)
- Client GUIDs and other identifiers (e.g., **c=mfa&c=mfa.gov&c=mfa**)

 example string:

```
e=Access&y=Guest&h=instance-sy9at2-relay.screenconnect.com&p=443&c=mfa&c=mfa.gov&c=mfa&c=pc
```

The attacker opens **instance-sy9at2-relay.screenconnect.com** and is able to remotely control the victim computer, execute various commands and install tools, among a range of other actions.

![](1_GNEkufKMaJCL514I-vJmUg.png)

---

MuddyWater’s use of remote access tools extends beyond **ScreenConnect** to include Remote Utilities under a similar attack methodology. The group delivers Remote Utilities in phishing campaigns using **PDF** files as decoys, contrasting with their ScreenConnect campaigns where the phishing lures are embedded in **DOC** documents.

In this Remote Utilities campaign, the phishing email contains a PDF decoy designed to entice the target to download a ZIP archive. This archive carries the Remote Utilities installation package, which, once run, installs the remote access tool on the victim’s system, enabling the attacker to stealthily control the compromised machine.

![](0_dMCX-LpjOCxiwstk.png)

---

The file **RutServ.exe** used by MuddyWater functions as part of their remote access tool deployment. When executed, **RutServ.exe** generates a unique identifier known as an Internet-ID and sends this information to the attacker’s mailbox. This Internet-ID acts as a key for the attacker to remotely connect back to the infected host.

![](0_egnx-_ieq3CmY6BE.png)

---

### N-Able

**Starting in October 2023**, the MuddyWater group shifted to using **N-Able’s** Advanced Monitoring Agent in their cyber-espionage campaigns. This new tactic continued to rely on **spear-phishing** emails to trick victims into downloading malicious samples, but with notable changes in payload hosting and delivery techniques.

Instead of commonly used file-sharing platforms like **OneHub**, MuddyWater began hosting their malicious payloads on **Storyblok**, a legitimate file-sharing website. The downloaded payloads no longer consisted of direct MSI installation packages. Instead, the infection chain involved a hidden directory structure orchestrated by a malicious **LNK** (shortcut) file.

You can read our fully detailed blog about [**.LNK**](https://darkatlas.io/blog/how-shortcut-files-lnk-used-to-deliver-ransomware)Files.

When a victim interacts with the phishing material, they are induced to open a ZIP archive containing this multi-layered setup. Inside, they find hidden folders and files, including the deceptive LNK file named Attachments.lnk. This LNK file triggers the execution of Diagnostic.exe, which then launches the legitimate Windows.Diagnostic.Document.EXE located in a hidden subfolder. This executable is a signed installer for the N-Able Advanced Monitoring Agent.

![](0_5hxHpy37qOJXLT5F.png)

---

The Diagnostic.exe file in **MuddyWater’s** campaign serves a dual purpose: it simultaneously opens the decoy document and executes the **N-Able** RMM installer hidden within the delivery package. This clever tactic maintains the illusion of legitimacy, as the victim sees a **genuine-looking** official memo from the Israeli Civil Service Commission (**ICSC**) discussing procedures related to government employees’ social media activities.

![](1_16XYzJeW53iQitvzRHYP9Q.png)

---

![](0_ak8a700CB3B_E7Qf.png)

---

---

The **N-Able** client program used by **MuddyWater** is a legitimate remote monitoring and management (RMM) tool that attackers configure through their server’s control panel to generate customized Agent installers. Once the victim runs the N-Able client and it installs on their system, the Agent actively connects back to the attacker-controlled N-Able management console.

**N-Able’s** legal functionalities encompass a wide array of **IT management** tasks, including:

- Remote system monitoring and health checks
- Backup management
- Security oversight
- Network management and troubleshooting

![](0_snGsU3m6iPjsEJ-_.png)

---

### Syncro

MuddyWater began using the **Syncro** remote administration tool as early as **September 2022**. This marked an evolution in their attack methods, diversifying the remote management tools they abuse. Their campaigns involve spear-phishing emails with attachments in various formats, including PDF, Office documents, and notably HTML files.

The use of HTML files as phishing payloads stands out because these files often bypass email security products more easily than executables or archives. HTML attachments are typically overlooked in phishing awareness training and do not raise immediate suspicion among recipients, increasing the chances of successful compromise.

![](0_2zG22QYkhlUZtK8u.png)

Two phishing messages linked to MuddyWater carried a malicious link and an HTML attachment. The HTML page was crafted to mimic an internal file hosting site for **egyptianabrasives[.]com**, luring victims to click a download button. The download link embedded in this page was:

[“https[:]//1drv.ms/u/s!Ah4-vpXOyPCGdd1DkLHmbL2qXQU?e=](https://1drv.ms/u/s!Ah4-vpXOyPCGdd1DkLHmbL2qXQU?e=RkaudW)xxxxx”

This link directs users to a file hosted on Microsoft OneDrive, a legitimate cloud storage service, which helps evade security detections. This setup is part of MuddyWater’s strategy to carefully disguise their payload delivery by spoofing trusted internal resources and leveraging reputable hosting platforms, increasing the likelihood that targeted individuals will trust the content and engage with the download.

![](0_dj3y2lWCFs1sbc28.png)

---

From these two URLs —

- The malicious link in the message body:  
  `https://www.dropbox[.]com/s/scj6n0l58yyb3f1/Purchase%20Order%20for%20Supplies--no12305570.zip?dl=0`
- The download link in the HTML attachment:  
  `https://1drv.ms/u/s!Ah4-vpXOyPCGdd1DkLHmbL2qXQU?e=RkaudW`

— it is evident that the attackers use public, legitimate file hosting services like Dropbox and Microsoft **OneDrive** for payload delivery. This tactic reduces the likelihood of interception or blocking by security software since traffic to these trusted domains is usually allowed and less scrutinized.

The payload downloaded from these hosted archives is an installer of Syncro, a legitimate remote monitoring and management (RMM) tool. The Syncro installer carries a digital signature and is not inherently malicious by itself. However, embedded in its configuration information within the MSI file are critical identifiers like **API\_KEY** and **CUSTOMER\_ID**, which tie the installed agent to the **attacker’s controlled** management server.

![](0_x8xrPawdIbnlzLEt.png)
![](1_repWpjENqDSoiL2JTWJcPA.png)

---

---

### **MITRE ATT&CK® techniques used by the MuddyWater group (G0069)**, suitable for embedding in your blog:

| **Tactic** | **Technique (ID)** | **Description** |
| --- | --- | --- |
| **Initial Access – Phishing** | Spearphishing Attachment (T1566.001) | Use of spear-phishing emails with malicious attachments via compromised accounts. |
| **Initial Access – Phishing** | Spearphishing Link (T1566.002) | Phishing via links delivered in targeted emails. |
| **Initial Access – Exploitation** | Exploit Public-Facing Application (T1190) | Exploitation of Microsoft Exchange (CVE-2020-0688). |
| **Initial Access – Exploitation** | Exploitation for Client Execution (T1203) | Exploitation of Office vulnerability (CVE-2017-0199). |
| **Initial Access – Exploitation** | Exploitation of Remote Services (T1210) | Exploitation of Netlogon vulnerability (CVE-2020-1472). |
| **Execution – Scripting** | PowerShell (T1059.001) | Use of PowerShell scripts for command execution. |
| **Execution – Scripting** | Windows Command Shell (T1059.003) | Use of cmd.exe and custom reverse shells. |
| **Execution – Scripting** | Visual Basic (T1059.005) | VBScript or macro execution for payloads (e.g., POWERSTATS). |
| **Execution – Scripting** | Python (T1059.006) | Use of Python-based tools like “Out1”. |
| **Execution – Scripting** | JavaScript (T1059.007) | JavaScript execution of payloads. |
| **Defense Evasion – Obfuscation** | Obfuscated Files or Information (T1027) | Code obfuscation (Base64, PowerShell obfuscation, steganography). |
| **Defense Evasion – Masquerading** | Match Legitimate Resource Name (T1036.005) | Naming files or registry entries to mimic Windows Defender. |
| **Persistence – Autostart** | Registry Run Keys / Startup Folder (T1547.001) | Persistence via registry run key. |
| **Persistence – Hijack Flow** | DLL Side-Loading (T1574.001) | Use of side-loaded DLLs for persistence. |
| **Persistence – Scheduled Tasks** | Scheduled Task (T1053.005) | Scheduled tasks used to maintain persistence. |
| **Persistence – Office Macros** | Office Template Macros (T1137.001) | Persistence via Word template macros (Normal.dotm). |
| **Discovery – Account Enumeration** | Domain Account Discovery (T1087.002) | Enumerating domain users via `net user /domain`. |
| **Discovery – Process Enumeration** | Process Discovery (T1057) | Listing running processes. |
| **Discovery – System Info** | System Information Discovery (T1082) | Gathering OS version and machine name. |
| **Discovery – Network Config** | System Network Configuration (T1016) | Collecting IP and domain information. |
| **Discovery – Network Connections** | System Network Connections (T1049) | Checking network connections (e.g., Skype). |
| **Discovery – User Enumeration** | System Owner/User Discovery (T1033) | Capturing user name on the system. |
| **Credential Access – Dumping** | OS Credential Dumping: LSASS (T1003.001) | Using Mimikatz and procdump. |
| **Credential Access – Dumping** | OS Credential Dumping: LSA Secrets (T1003.004) | Using LaZagne. |
| **Credential Access – Dumping** | OS Credential Dumping: Cached (T1003.005) | Using LaZagne for cached credentials. |
| **Credential Access – Password Stores** | Credentials from Password Stores (T1555) | Extracting stored passwords from email or browser. |
| **Data Staging** | Local Data Staging (T1074.001) | Storing decoy PDFs in %temp%. |
| **Command & Control – HTTP** | Application Layer Protocol: Web (T1071.001) | C2 communications conducted over HTTP. |
| **Command & Control – Proxy Usage** | External Proxy (T1090.002) | Use of proxy networks to hide C2 servers. |
| **Command & Control – Tool Transfer** | Ingress Tool Transfer (T1105) | Uploading additional tools to compromised systems. |
| **Exfiltration** | Exfiltration Over C2 Channel (T1041) | Data exfiltration through C2 infrastructure. |
| **Impact – Archive** | Archive Collected Data (T1560.001) | Using makecab.exe to compress data. |
| **Encryption** | Encrypted Channel: Symmetric Cryptography (T1573.001) | Using AES to encrypt C2 responses. |
| **Data Encoding** | Standard Encoding (T1132.001) | Encoding C2 communications with Base64. |

---

---

**IOCs**

```
kinneretacil.egnyte[.]com  
salary.egnyte[.]com  
gcare.egnyte[.]com  
rimonnet.egnyte[.]com  
alltrans.egnyte[.]com  
megolan.egnyte[.]com  
bgu.egnyte[.]com  
fbcsoft.egnyte[.]com  
cnsmportal.egnyte[.]com  
alkan.egnyte[.]com  
getter.egnyte[.]com  
ksa1.egnyte[.]com  
filecloud.egnyte[.]com  
nour.egnyte[.]com  
airpazfly.egnyte[.]com  
cairoairport.egnyte[.]com  
silbermintz1.egnyte[.]com  
smartcloudcompany[.]com  
onlinemailerservices[.]com  
smtpcloudapp[.]com  
softwarehosts[.]com  
airpaz.egnyte[.]com  
airpazflys.egnyte[.]com  
fileuploadcloud.egnyte[.]com  
downloadfile.egnyte[.]com  
https://shorturl[.]at/NCxJk  
https://shorturl[.]at/bYqUx  
https://ws.onehub[.]com/files/bbmiio1c  
https://ws.onehub[.]com/files/zgov9aqy  
146.19.143[.]14  
91.235.234[.]202  
85.239.61[.]97  
95.164.32[.]69  
5.252.23[.]52  
194.4.50[.]133  
193.109.120[.]59  
89.221.225[.]81  
45.150.108[.]198  
200.200.200[.]248  
169.150.227[.]230  
169.150.227[.]205  
185.248.85[.]20  
141.98.252[.]143  
31.171.154[.]54  
146.70.172[.]227  
198.54.131[.]36  
73c677dd3b264e7eb80e26e78ac9df1dba30915b5ce3b1bc1c83db52b9c6b30e  
960d4c9e79e751be6cad470e4f8e1d3a2b11f76f47597df8619ae41c96ba5809  
b8703744744555ad841f922995cef5dbca11da22565195d05529f5f9095fbfca  
94278fa01900fdbfb58d2e373895c045c69c01915edc5349cd6f3e5b7130c472  
5df724c220aed7b4878a2a557502a5cefee736406e25ca48ca11a70608f3a1c0  
39da7cc7c627ea4c46f75bcec79e5669236e6b43657dcad099e1b9214527670e  
c23f17b92b13464a570f737a86c0960d5106868aaa5eac2f2bac573c3314eb0f  
fb58c54a6d0ed24e85b213f0c487f8df05e421d7b07bd2bece3a925a855be93a  
7e6b04e17ae273700cef4dc08349af949dbd4d3418159d607529ae31285e18f7  
ff2ae62ba88e7068fa142bbe67d7b9398e8ae737a43cf36ace1fcf809776c909  
e2810cca5d4b74e0fe04591743e67da483a053a8b06f3ef4a41bdabee9c48cf7  
90f94d98386c179a1b98a1f082b0c7487b22403d8d5eb3db6828725d14392ded  
20aaeac4dbea89b50d011e9becdf51afc1a1a1f254a5f494b80c108fd3c7f61a  
55af6a90ac8863f27b3fcaa416a0f1e4ff02fb42aa46a7274c6b76aa000aacc2  
f925d929602c9bae0a879bb54b08f5f387d908d4766506c880c5d29986320cf9  
424a9c85f97aa1aece9480bd658266c366a60ff1d62c31b87ddc15a1913c10e4  
c80c8dd7be3ccf18e327355b880afb5a24d5a0596939458fb13319e05c4d43e9  
c88453178f5f6aaab0cab2e126b0db27b25a5cfe6905914cc430f6f100b7675c  
31591fcf677a2da2834d2cc99a00ab500918b53900318f6b19ea708eba2b38ab  
a0968e820bbc5e099efd55143028b1997fd728d923c19af03a1ccec34ce73d9b  
88788208316a6cf4025dbabbef703f51d77d475dc735bf826b8d4a13bbd6a3ee  
4064e4bb9a4254948047858301f2b75e276a878321b0cc02710e1738b42548ca  
e7896ccb82ae35e1ee5949b187839faab0b51221d510b25882bbe711e57c16d2  
1c0947258ddb608c879333c941f0738a7f279bc14630f2c8877b82b8046acf91  
8fbd374d4659efdc5b5a57ff4168236aeaab6dae4af6b92d99ac28e05f04e5c1  
7e14ca8cb7980e85aff4038f489442eace33530fd02e2b9c382a4b6907601bee  
02060a9ea0d0709e478e2fba6e9b71c1b7315356acc4f64e40802185c4f42f1c  
53b4a4359757e7f4e83929fba459677e76340cbec7e2e1588bbf70a4df7b0e97  
0ab2b0a2c46d14593fe900e7c9ce5370c9cfbf6927c8adb5812c797a25b7f955  
https://ws.onehub[.]com/files/x68hqy91  
https://ws.onehub[.]com/files/97lrcyvc  
https://ws.onehub[.]com/files/gts7uevh  
https://ws.onehub[.]com/files/v5ww52ne  
https://ws.onehub[.]com/files/kwdphknm  
https://freeupload[.]store/rALE7/wIHItUcE08.msi/download  
https://kinneretacil.egnyte[.]com/fl/gRykrFURtE  
https://filetransfer[.]io/data-package/tuMe19fV/download  
https://ws.onehub[.]com/files/mz8ok6gf  
http://a.storyblok[.]com/f/259791/x/91e2f5fa2f/attachments.zip  
https://a.storyblok[.]com/f/259837/x/21e6a04837/defense-video.zip  
https://ws.onehub[.]com/files/94otjyvd  
https://ws.onehub[.]com/files/7w1372el  
instance-sy9at2-relay.screenconnect[.]com  
instance-uwct38-relay.screenconnect[.]com  
https://1drv[.]ms/u/s!Ah4-vpXOyPCGdd1DkLHmbL2qXQU?e=RkaudW  
https://www.dropbox[.]com/s/scj6n0l58yyb3f1/Purchase%20Order%20for%20Supplies--no12305570.zip?dl=0  
https://a.storyblok[.]com/f/259791/x/94f59e378f/questionnaire.zip  
51.255.19[.] 178:443  
51.254.25[.] 36:443  
178.32.30[.] 3:443  
146.70.149[.] 61:8008  
193.109.120[.] 59:8008
```

---

---

**Conclusion**

MuddyWater is a highly persistent Iranian state-sponsored cyber espionage group aligned with the Ministry of Intelligence and Security (MOIS), active since at least **2017**. The group uses a sophisticated blend of social engineering, legitimate remote administration tools, and custom malware to breach and maintain long-term access to targeted networks—primarily across the Middle East but also globally.

Their campaigns rely heavily on spear-phishing from compromised email accounts, deploying malware such as **PowGoop, Small Sieve, Canopy, Mori, POWERSTATS**, and their custom **BugSleep** backdoor. They frequently abuse commercial Remote Monitoring and Management (RMM) software like **Atera Agent**, **ScreenConnect**, Remote Utilities, **N-Able**, and **Syncro** to obfuscate their activities and evade detection.

**MuddyWater** targets key sectors including government agencies, municipalities, airlines, travel industries, and journalists. Their operational sophistication includes exploiting known vulnerabilities in public-facing applications and remote services, using obfuscated PowerShell and scripting tools, DLL side-loading, and leveraging encrypted, encoded command and control channels.

Organizations are advised to enhance defenses by monitoring for indicators of compromise tied to this threat actor, applying relevant patches promptly, training personnel on phishing awareness, and scrutinizing the use of legitimate **RMM** platforms within their networks.

**MuddyWater’s** evolving arsenal and adapting tactics make it a persistent threat requiring continued vigilance and proactive cybersecurity measures.
