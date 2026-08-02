---
title: "Suspicious ScreenConnect Abuse by Threat Actors"
date: 2025-10-12 11:33:40 +0200
categories: [Threat Intelligence]
tags: [darkweb, threat-actors]
image:
  path: screenconnect-1500.webp
  alt: "Suspicious ScreenConnect Abuse by Threat Actors"
media_subpath: /assets/img/posts/screen-connect-full-analysis
toc: true
---

Recently observed an uptick in threat actors abusing **RMM** tools for initial access via phishing. I decided to investigate several popular **RMMs** — **AnyDesk**, **ConnectWise ScreenConnect**, and \*\*Atera \*\*— and published my findings on how APT groups abuse these platforms in my [**DarkAtlas**](https://darkatlas.io/blog/muddywater-inside-irans-persistent-cyber-espionage-group-targeting-the-middle-east) research. If you’re tracking modern intrusion trends, these tools are worth watching closely.

**Why RMMs Are Abused**

RMM platforms provide **remote access, unattended control, file transfer, and scripting**. While built for IT management, attackers frequently repurpose them for **initial access, persistence, remote control, and lateral movement**. Their administrative power, combined with **custom installers, invite links, and public URLs**, makes them high-value targets — and a critical focus for **DFIR and threat hunting**.

**AnyDesk: Declining but Still Abused**

I recently came across a **CyberTriage blog** discussing **AnyDesk**. However, many threat actors have moved away from AnyDesk because it has become **easier to detect**.

**Investigating ScreenConnect Abuse**

That shift led me to investigate **ScreenConnect**, which has become quite trendy among adversaries. I started with the free edition (not sure if it behaves exactly like the paid version), but I still wanted to dive in and see how it could be abused.

![](1_w_fpDesu50gSmhJ29VUIRA.png)

---

**ScreenConnect** is an **RMM** solution developed by **ConnectWise** that **administrators** use to deploy and run remote tasks across endpoints.

While it’s intended to simplify management (often as an alternative to **WMI**), adversaries have learned to abuse it for **initial access**, **remote control**, **persistence**, and **lateral movement** — so it’s become an important tool to monitor in DFIR and threat hunting

---

**ScreenConnect Capabilities**

**ScreenConnect** (by ConnectWise) enables **platform-independent remote access** across:

- Windows
- macOS
- Linux
- iOS
- Android
- and more

**Key Features include:**

- VPN functionality
- REST API integration
- File transfer
- Session logging
- Remote printing
- Unattended access

---

### ScreenConncet Indicators of Existence

**Installer Artifact**:

```
ScreenConnect.ClientSetup.msi
```

**Known path(s):**

```
C:\Users\Kh4lifa\AppData\Local\Temp\ScreenConnect\25.4.20.9295\760c1fc14562a55f\ScreenConnect.ClientSetup.msi
```

? The installer observed for ScreenConnect is an `.msi` package that appears to execute **primarily** **in-memory**, reducing on-disk artifacts and making basic signature/AV checks less effective. Attackers favor this technique because it lowers the visibility of installation and persistence actions to traditional tools that scan files on disk.

---

### Delivery Methods Attackers Exploit

During deployment, **ScreenConnect** presents a **management panel** that allows an administrator to create a **custom access URL** (for example: `kh4lifa.test.com`).

![](0_GjXmXK1H1yiYp4Xd.png)

Attackers abuse this by:

- Hosting **phishing pages**
- Using **invite links** to lure victims
- Deploying **custom installers** that mimic legitimate workflows

Because the **builder and invite links** can be generated directly from the console, adversaries gain a **flexible phishing surface**.

![](0_Ag7DDFc8bJ1dKfN-.png)

---

On the top-left of the ScreenConnect management panel there is a **Build+** option that lets operators create a customized “builder.”

This builder can be configured to either install the agent directly or to generate an invite link that walks a target through multiple stages to enroll the agent.

Because builders and invite links can be created and customized from the console, they provide a flexible delivery surface that attackers may abuse to craft staged phishing flows or to mask enrollment activity in legitimate remote-management workflows.

https://kh4lifa.test.screenconnect.com/Bin/ScreenConnect.ClientSetup.exe?e=Access&y=Guest

![](0_Xq3oKc6JSuZe1tHj.png)

---

After deployment, the ScreenConnect installer drops a Windows client binary (commonly observed as a `WindowsClient` executable) which launches and registers itself as a running service/process to provide remote connectivity. Because the agent is installed and executed on the endpoint, defenders should treat this binary as **the primary artifact for detection**, telemetry collection, and incident response.

```
C:\Program Files (x86)\ScreenConnect Client (760c1fc14562a55f)\ScreenConnect.WindowsClient.exe
```

![](1_-ySkhBN5YKYcnuj4Q-UMuQ.png)

When executed, the ScreenConnect client launches a process named

```
ScreenConnect.WindowsClient.exe
```

![](1_w2pCM6e1SkIbTsi3NfB8Mw.png)

```
C:\Program Files (x86)\ScreenConnect Client (760c1fc14562a55f)\ScreenConnect.WindowsClient.exe
```

---

### Config/Log Files

**USER** Log file

**Filename (context):** `user.config` — a ScreenConnect client configuration file.  
**Type:** XML configuration (System.Configuration client settings).  
**Purpose:** maps hostnames (custom access URLs) to resolved IP addresses and records a timestamp for when that mapping was observed/created.

**Path:**

```
C:\Windows\SysWOW64\config\systemprofile\AppData\Local\ScreenConnect Client (760c1fc14562a55f)\user.config
```

![](1_k4NOG4rERpEG-sYTxjY4JA.png)

---

> *This IP appears to be malicious and was used to communicate with suspicious domains.*

![](1_UjJpax9_KOwwDDN17nwH8Q.png)

---

### System.conf

- **Filename (context):** `system.config` – a ScreenConnect core configuration file.

![](1_wRIMpGfNqwX6KwLGskkEbw.png)

- **Type:** XML configuration (application and client launch parameters).
- **Purpose:** stores connection settings, including hostnames/IPs, ports, and encrypted launch keys that define how the ScreenConnect client connects to its server.
- **Path:**

```
C:\Windows\SysWOW64\config\systemprofile\AppData\Local\ScreenConnect Client (760c1fc14562a55f)\user.config
```

![](1_hpOaBUjIIAGprmrf9poGiA.png)

---

---

After the initial connection of the ScreenConnect, a Security event is generated, recording Event ID **4573**

However, this evidence alone is not sufficient for a full investigation. To gain deeper insights, I will extend the analysis and examine additional data sources and system artifacts.

---

After the remote session was established, Application Log events with IDs **100** and **101** were recorded. For deeper analysis, we can focus on the details of Event ID 100.

![](1_uLAgaWsPpU6y5ZdQhY5NBQ.png)

---

We can now examine Event ID **101** for further insights.

![](0_H-vTAerod8j5hLJy.png)

---

---

I also searched for any files that might record the chat but did not find any. However, during memory analysis, I was able to recover the chat data. Unlike AnyDesk, which stores chat logs in configuration files, ScreenConnect stores them in memory, making memory acquisition essential for retrieving chat artifacts.

![](0_PPSs7UWA7zKqdgVu.png)

AnyDesk chat files created

---

### File Transfer

Files can also be transferred directly through the ConnectWise web interface.

![](0_havntpw0NCq-6v79.png)

---

**Sending Files**

A file was sent to the client using the host software. This action resulted in the creation of a new folder located at `C:\Users\Kh4lifa\Documents\ConnectWiseControl\Files`, which contained the transferred file.

![](1_toMMh2mPEmxgW34ZFKDyOg.png)

Event **201** Recorded while sending a file

---

**Receiving files**

While receiving file from the victim machine there’s no event’s id collected.

but there’s an edit occurred to the user.config file.

---

### Conclusion

Like many legitimate RMM platforms, **ScreenConnect is powerful — and that power makes it attractive to adversaries**.

My investigation shows attackers exploit:

- **Custom URLs, invite links, and builders**
- **Low disk footprint installers**
- **Persistent Windows clients and configs**
- **Memory-only artifacts like chat logs**

? For defenders, **monitoring these indicators and logs is critical** in DFIR and **threat hunting investigations**.

? *Learn how DarkAtlas helps enterprises detect and respond to RMM abuse — [see our Security Products](https://darkatlas.io/products)*
