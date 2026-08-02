---
title: "Smishing Triad Targets Egypt’s Financial Sector and Postal Services"
date: 2025-11-24 14:50:17 +0200
categories: [Infrastructure adversary hunting, Threat Intelligence]
tags: [investigation, threat-actors]
image:
  path: GettyImages-1433299887-scaled.webp
  alt: "Smishing Triad Targets Egypt’s Financial Sector and Postal Services"
media_subpath: /assets/img/posts/smishing-triad-targets-egypts-financial-sector-and-postal-services
toc: true
---

Recently, during one of our threat hunting operations, our squad identified multiple malicious domains impersonating major Egyptian service providers, including **Fawry**, the **Egypt Post**, and **Careem**. These domains were likely established to support fraud, phishing campaigns, and other malicious activities targeting users and organizations.

Before we begin our analysis, we will provide an overview of the **Smishing Triad**, the cybercriminal group relevant to this report.

The Smishing Triad is a Chinese-speaking cybercriminal group specializing in large-scale **smishing campaigns** (SMS-based phishing) targeting victims worldwide. The group is primarily known for impersonating **national postal services, logistics companies, and delivery providers**, sending fraudulent messages that claim a package is delayed, requires additional fees, or needs address confirmation.

Here’s more information about the scam pages we identified.

![](1_DwmS2WPrcyKCPs15BVkP0w.png)
![](1_TXT9KpNeQwOcaxmB4v3L0g.png)

---

The **Smishing Triad** operates globally, deploying identical scam pages across multiple countries that impersonate **government services, postal offices, and financial institutions** to steal sensitive information from unsuspecting victims.

![](image-898x1024.png)

---

As we expanded our investigation to uncover additional domains impersonating service providers worldwide, we began by analyzing the HTTP headers of the identified infrastructure. We then leveraged these indicators to craft a Shodan query, enabling us to discover further malicious domains and related assets.

In addition, our investigation revealed multiple domains specifically impersonating **Fawry**, highlighting the group’s focus on targeting financial service providers.

![](1_G3dR03DV5z8mUur5VYfybw.png)

---

During our exploration of **AS132203 (Tencent Building, Kejizhongyi Avenue)**, we discovered additional domains impersonating **egyptpost.gov.eg**, further illustrating the Smishing Triad’s extensive use of shared infrastructure to target postal services.

![](1_HCDbWJrR1irrIfAqwzfxCQ.png)

---

The same **AS132203** infrastructure is also being used to host phishing pages impersonating **UnionPay, Careem, and TikTok**, demonstrating the Smishing Triad’s extensive abuse of shared resources for multiple campaigns.

![](1_BeqdHGWQXzIeUsl7oX0TJw.png)

---

In addition, a large number of other phishing and scam pages reside within the same AS, with multiple examples documented here: [**scampages**](https://www.nksc.lt/doc/vasaris/siena-nksc.txt).

---

We will not be conducting a deep dive into the infrastructure hosting these scam pages; instead, our focus will shift toward uncovering the actors behind them and identifying which **phishing-as-a-service (PhaaS) vendor** is providing these scam kits.

---

First, we need to understand where the **Smishing Triad** distributes and sells their scam services. Our investigation revealed that they primarily operate through **Telegram**, where they advertise and sell their phishing kits and related services.

![](0_v8Jz1mOU1zjLrOxI.png)

smished triad tg group

---

Through their older Telegram channels, we identified a video from a member known as **“wangduoyu8”**, in which they demonstrate how their **phishing-as-a-service (PhaaS)** platform operates.

![](1_BN4QAbdmP2eaqSnufXkwbQ.png)

---

![](0__GJdtE8gBCmb_uma.png)

---

### Panda Smishing Kit

The smishing kit can be fully customized and deployed on a virtual server. Once the operator provides the required credentials, the kit is automatically unpacked and installed, preparing the environment for immediate use.

![](0_vKF0NjbMmrhp2QjK.png)

---

Beyond U.S. service impersonation, the smishing kit offers a wide range of international templates, including those that mimic prominent ISPs such as **Du (UAE)**. These templates are designed to harvest PII from victims across different regions, significantly expanding the campaign’s global reach.

![](0_MZKB7x8Ducrk3Sl7.png)

---

Here are **example smishing message templates** that align with the brands you listed, written safely for analysis and reporting purposes (NOT usable as functional phishing messages):

---

### AT&T

> *AT&T Alert: Unusual activity detected on your account. To verify your details, please confirm your information at: att‑secure‑verify[.]com*

![](0_SKfihZQeQ1TgVHiG.png)

---

### DHL

> *DHL: Your package is awaiting delivery. Additional shipping fee required. Complete payment here: dhl‑express‑update[.]com*

---

### Evri

> *Evri: We attempted delivery today but no one was home. Reschedule delivery at: evri‑redelivery‑info[.]com*

---

### UPS

> *UPS Notice: Your parcel cannot be delivered due to missing address details. Update your information: ups‑track‑update[.]com*

---

### USPS

> *USPS: Your package is on hold. Please confirm your address within 24 hours: usps‑delivery‑confirm[.]com*

![](0_rxg7MlRIQB-WMMu6.png)

---

### Movistar

> *Movistar: Your mobile service will be suspended due to unpaid charges. Verify payment: movistar‑billing‑secure[.]com*

---

### UK Government Parking Fines

> *GOV.UK: You have an outstanding parking fine. Pay now to avoid additional penalties: gov‑parking‑payment[.]uk*

---

### Vodafone

> *Vodafone: Your account will be deactivated due to failed billing. Update details: vodafone‑secure‑verify[.]com*

---

![](0_5m1VNymtTDuI-UYV.png)

---

### Darcula PhaaS can now auto-generate phishing kits for any brand

Last year, **Darcula** emerged as a large-scale phishing-as-a-service (PhaaS) operation, leveraging over **20,000 domains** that spoof well-known brands to steal credentials from **Android and iOS users in more than 100 countries**.

Netcraft warns that a significantly more powerful version is already in development, and cybercriminals are actively exploring it even before its official release.

![](0_gYfcATqkuskW66DG.jpg)

---

The fraudster can selectively modify key elements of a legitimate website — such as login fields, payment forms, and two-factor authentication prompts — and replace them with phishing pages designed to capture sensitive information. They may also inject custom error messages or alter JavaScript functionality to intercept and exfiltrate user input in real time.

The Darcula Suite streamlines this process by providing pre‑built templates, including fake password reset pages, credit card payment forms, and 2FA code entry screens, allowing attackers to quickly deploy convincing phishing workflows with minimal effort.

![](0_qxu7hmXoeBdm38v8.jpg)

---

Once the kit is complete, it is uploaded to the Darcula admin panel, enabling streamlined deployment, centralized control, real‑time data harvesting, and performance monitoring.

Beyond the new DIY system, Darcula 3.0 introduces several notable enhancements:

- **Anti‑detection measures**, including randomized deployment paths, IP filtering, crawler blocking, and device‑type restrictions to evade automated scanning and security tools.
- **An upgraded admin panel** featuring simplified phishing campaign management, a performance dashboard, real‑time logs of stolen credentials, and Telegram notifications triggered when victims submit sensitive data.
- **A card cloning utility** that converts stolen credit card information into virtual card images that can be added directly to digital payment applications.

According to Netcraft, Telegram groups associated with Darcula are already advertising burner phones preloaded with multiple stolen cards, indicating growing adoption and commercialization of this latest version.

![](0_a74lIhhwkuCPgRkn.jpg)

---

![](1_mz2YLZ4BPoX5PWtzbyj_1Q.png)

The introduction of Darcula 3.0 and its powerful new features make detecting and stopping phishing campaigns even more challenging, while the ease of use of the latest version guarantees that phishing volumes will increase.

---

The latest iteration of the Darcula platform introduces advanced AI-driven capabilities, enabling operators to automatically create phishing pages with a single click, greatly reducing the effort and expertise required to launch campaigns.

![](1_7fnrHD4FAp93zsMvS8T4vQ.png)

---

**Conclusion**

The Smishing Triad and emerging PhaaS operations like **Darcula** highlight the evolving sophistication of global phishing campaigns. By leveraging advanced tools, AI-driven templates, and widespread infrastructure, these groups are able to target users across multiple countries and industries with unprecedented efficiency.

Our investigation underscores the importance of proactive threat hunting, continuous monitoring of phishing infrastructure, and user awareness to mitigate the risks posed by these campaigns. As cybercriminals continue to innovate, understanding their tactics, techniques, and procedures is essential for building resilient defenses and protecting sensitive information worldwide.

---

### IOCs

```
egyptpost.baby  2025-11-21  
egyptpost.bond  2025-11-18  
egyptpost.icu  2025-11-18  
egyptpost.pics  2025-11-21  
egyptpost.quest  2025-11-21  
egyptpost.rest  2025-11-21  
egyptpost.skin  2025-11-21  
fawry.autos  2025-11-18  
fawry.baby  2025-11-23  
fawry.boats  2025-11-23  
fawry.bond  2025-11-13  
fawry.cfd  2025-11-06  
fawry.click  2025-11-07  
fawry.club  2025-11-18  
fawry.cyou  2025-11-07  
fawry.help  2025-11-09  
fawry.lat  2025-11-09  
fawry.life  2025-11-23  
fawry.lol  2025-11-13  
fawry.love  2025-11-09  
fawry.mom  2025-11-18  
fawry.qpon  2025-11-09  
fawry.quest  2025-11-23  
fawry.rest  2025-11-18  
fawry.sbs  2025-11-13  
fawry.skin  2025-11-23  
fawry.top  2025-11-07  
jumia.cfd  2025-11-19  
tikt.help  2025-11-18  
unionpay.cfd
```
