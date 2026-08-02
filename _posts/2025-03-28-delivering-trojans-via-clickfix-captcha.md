---
title: "Delivering Trojans Via ClickFix Captcha"
date: 2025-03-28 00:20:32 +0200
categories: [Malware Analysis, Threat Intelligence]
tags: [malware-analysis]
image:
  path: WhatsApp-Image-2025-04-20-at-2.19.41-AM.jpeg
  alt: "Delivering Trojans Via ClickFix Captcha"
media_subpath: /assets/img/posts/delivering-trojans-via-clickfix-captcha
toc: true
---

### Overview

Recently, a new social engineering technique has emerged, rapidly gaining traction as a highly effective method for delivering various types of malware, including **Infostealers**, **Ransomware**, and **Quakbot**. This technique exploits a seemingly harmless element — a **ClickFix Captcha** — to deceive users and bypass traditional security measures.

## Quakbot (Qbot) — The Evolving Banking Trojan

**First discovered in 2008**, Quakbot (Qbot) is a sophisticated banking trojan that has undergone continuous development, with periods of dormancy followed by renewed activity. Despite occasional gaps in operational use, it remains one of the most effective and versatile malware families, regularly updated with new capabilities and techniques to evade detection and enhance persistence.

[**DarkAtlas Research Squad**](https://darkatlas.io/) is set to present a real-world scenario demonstrating how **QakBot** is being delivered through the **ClickFix Captcha** technique. This presentation will provide an in-depth analysis of how attackers leverage seemingly legitimate captchas to bypass user suspicion and execute malicious payloads.

**protectedsound[.]digital** redirects to a **ClickFix** captcha at **cfcaptcha[.]com**

![](1_AIYIopEvOhNLQVDp1EWheQ.png)

Quakbot being delivered through ClickFix Captcha, where the captcha tricks the user into performing an unsuspecting activity on their local machine by using the **Windows key + R** and executing a malicious command preloaded into the clipboard.

![](1_Mggb9D9a-7hcfvmMBuZi9Q.png)

The command attempts to download a text file from a specified URL and use its contents as input for the next command. The `iex` at the end of the URL stands for **Invoke-Expression**, a PowerShell command that executes the retrieved string as a PowerShell command, enabling the execution of malicious code directly from the downloaded file.

![](1_r32IaWED8YBigC4xd4ZuaQ.png)

While the contents of the file at **cfcaptcha[.]com/flwssetp.txt** are mostly encrypted, certain parts are seen in clear text and give insight into what the encrypted contents might be doing.

![](1_WZ10LZKb1BTGutPJzlvVRg.png)

This PowerShell command displays a graphical message box with the text **“Verification Complete!”** and an **“OK”** button. The intent is to deceive the user into believing that the verification process was successful, encouraging them to proceed on the website without suspicion.

![](1_4adt4JznPfODCTlaTpCAvQ.png)

Another section of the obfuscated content appeared to involve **XOR Decryption** of a long hex string, suggesting that the payload was encoded to evade detection and analysis. This technique is commonly used by malware to obfuscate malicious code, making it harder for security tools to identify and analyze the threat.

![](1_XaUsObURaMHlJctrOTcEzA.png)

decode the hex To get more Value.

![](1_zsRlqxPX0Rawdwk7HYBRwQ.png)

1- The decoded payload reveals a **PowerShell** script designed to:

2- Download a ZIP file from [**https://duolingos.com/flswunwa.zip**](https://duolingos.com/flswunwa.zip)**.**

3- Save the ZIP to the **$env:AppData** directory as flswunwa.zip.

4- Extract the ZIP using **Expand-Archive** to the same directory.

5- Load the .NET assembly **System.IO.Compression.FileSystem** to handle the ZIP file.

6- Open the ZIP file and likely execute its contents (though the full payload isn’t visible yet).

 — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —

We going to download “**hxxps://duolingos[.]com/flswunwa[.]zip**” Manully to Check it.

![](1_XbIFyksMzOx7iYEcUpRjUQ.png)

Fake Zip Dowloader

This technique allows **Qbot** operators to create the appearance of multiple files or subdirectories, such as:

**hxxps://duolingos[.]com/xxxxx[.]zip**

**hxxps://duolingos[.]com/yyyyy[.]zip**

**hxxps://duolingos[.]com/files/zzzzz[.]zip**

Purpose and Impact:  
**Endless Unique URLs**  
Attackers can generate an unlimited number of unique URLs for malware distribution, making it difficult for security solutions to blacklist or detect malicious activity effectively.

**Obfuscation of Malicious Code**The actual location of the malicious payload remains concealed, complicating efforts by security researchers and website owners to trace, analyze, and mitigate the threat.

This explains why executing **hxxps://duolingos[.]com/flswunwa[.]zip** in a sandbox environment failed to reveal meaningful details about the file.

**VirusTotal** analysis for **hxxps://duolingos[.]com/flswunwa.zip** — Detected by **1/96** security vendors as malicious. Status: **404 (Not Found)**, **Content type: text/html**, indicating possible obfuscation or removal.

![](1_92pyY8sR9_WhogrfSm6uhQ.png)

**URLScan** results for **hxxps://duolingos[.]com/flswunwa.zip** — 3 HTTP transactions observed, all returning **404 errors**. The site is hosted on **Cloudflare (188.114.96.3)**, indicating possible obfuscation or temporary removal of malicious content

![](1_HzJnpfDw-y28KOXRJ_p0Mw.png)

**Hybrid Analysis** report for **`hxxps://duolingos[.]com/flswunwa.zip`**— Marked as suspicious with a threat score of **50/100**. Detected phishing activity, network behavior involving **3** domains and **4** hosts, and **11** indicators mapped to **8** MITRE ATT&CK techniques and **5** tactics

![](1_0PF2QDLXBswlg4YW0jNNcQ.png)

In reality, all these requests are intercepted and redirected by a rewrite rule to a malicious ****PHP Script**** hosted on the compromised server. This **PHP Script** functions as a **Proxy**, dynamically fetching the actual malicious content from a secondary tier of attacker-controlled servers. By operating as an intermediary, the ****PHP Script**** conceals the true origin of the **Malicious Payload**, adding a layer of obfuscation and making it harder for defenders to trace the source of the attack.

In this particular case, the malicious **PHP Script** is embedded directly within the body of the page, further complicating detection and analysis. This tactic enables attackers to dynamically generate and serve malicious content, bypassing conventional security measures and increasing the resilience of the **Attack Infrastructure**.

![](1_Y24ry0QeiU0kIRxGlcI92A.png)

The file in question is a PHP-based **QakBot** dropper, designed to download and execute **QakBot** or other malware, such as stealer malware and ransomware, from a remote server onto the victim’s system. The dropper facilitates the execution of the malicious payload by either exploiting system vulnerabilities or using **Social Engineering** techniques to deceive the victim into allowing execution.

As of the time of publishing this article, the PHP dropper file has been removed, and the associated domains — **hxxps://duolingos[.]com** and **hxxp://cfcaptcha[.]com** — are in the process of being taken down. This action aims to disrupt the malware delivery infrastructure and limit further infections.

## Summary:

The success of **ClickFix** stems from its ability to exploit user trust in captchas, software updates, and websites that appear legitimate. This psychological leverage increases the likelihood of users unknowingly executing malicious commands on their local systems, thereby enabling attackers to gain a foothold and deploy additional payloads without raising suspicion.
