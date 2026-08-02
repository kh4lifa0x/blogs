---
title: "Scattered Spider – UNC3944: A Comprehensive and Detailed Threat Profile"
date: 2025-08-11 10:10:58 +0200
categories: [Threat Intelligence]
tags: [scattered-spiders, shinyhunters, threat-actors]
image:
  path: 553a4a28-11c1-49af-8fc0-ae2f447e9eff.png
  alt: "Scattered Spider – UNC3944: A Comprehensive and Detailed Threat Profile"
media_subpath: /assets/img/posts/scattered-spider-unc3944-a-comprehensive-and-detailed-threat-profile
toc: true
---

**Scattered Spider** (also known by aliases such as **0ktapus**, **Muddled Libra**, **Roasted 0ktapus**, **Scatter Swine**, **UNC3944**, **Octo Tempest**, **Storm-0971**, **DEV-0971**, and **Starfraud1**) is recognized as a highly active and rapidly evolving cybercriminal group, notable for its adaptability and sophistication. The group has been operational since at least May 2022 and is primarily financially motivated, orchestrating attacks for profit rather than ideological reasons.

---

**Who do they target?**

In late **April 2025**, several major UK retailers—including **Marks & Spencer**, **Co-op**, and **Harrods**—experienced a series of disruptive ransomware attacks attributed to Scattered Spider, an increasingly sophisticated and notoriously effective cybercriminal group. Although one retailer reportedly managed to thwart the breach attempt, most victims suffered significant operational disruptions, lost revenue, and extensive data breaches linked to the incident

Scattered Spider group behind the September 2023 ransomware attacks on **MGM** Resorts and Caesars Palace, demonstrated a striking blend of social engineering and technical exploitation. Their approach reflects the evolving landscape of cybercrime, targeting human vulnerabilities as much as technical ones.  
  
**Incident Timeline:**

**Late September:** Both companies restore normal operations.

**Early September 2023:** Both MGM and Caesars experience suspicious activity within their IT systems.

**September 7th:** Caesars suffers a data breach, acknowledging a social engineering attack targeting a third-party IT vendor.

**September 11th:** MGM faces a ransomware attack by the Scattered Spider (UNC3944) group, causing widespread disruption.

**September 14th:** Scattered Spider claims to have exfiltrated 6 terabytes of data from both companies.

**Mid-September:** Caesars reportedly pays a $15 million ransom, while MGM opts for collaboration with law enforcement.

---

**Scattered Spider TTPs**

## Phishing Kit Variations and Deployment

- **Multiple visually identical phishing kits:** The group adapts front-end presentation to mimic legitimate login portals, increasing trust and victim interactivity.
- **Distinct source code for each kit:** Despite similar appearances, kits are uniquely coded—sometimes to evade signature-based detection or hinder forensic analysis across incidents.
- **Dedicated server reuse:** Scattered Spider often utilizes the same servers across multiple campaigns, leveraging established infrastructure for rapid deployment and management.

#### 2. Domain Registration & Management Strategies

- **Bulk domain registration:** They routinely register clusters of domains within short windows (same day or consecutive days), allowing for coordinated multi-vector attacks that may target individual companies or several firms in the same industry.
- **Attack wave structuring:** Multiple domains are set to target the same organization, staggered over different attack waves to maximize persistence and campaign longevity.
- **Preferred Registrars & Hosts:**
  - Recent preferences: NiceNIC (registrar); Njalla, Virtuo, Cloudflare (hosting).
  - Historical choices: Porkbun, Namecheap, Hostinger, Tucows, Hosting Concepts.

#### 3. Hosting and Network Infrastructure

- **Preferred ASNs:** Their hosting infrastructure leverages networks such as Cloudflare (AS13335), Choopa (AS20473), DigitalOcean (AS14061), Hostinger (AS47583), Akamai-Linode (AS63949), and Namecheap (AS22612). These choices reflect a preference for resilient and privacy-focused hosting services capable of supporting rapid, large-scale phishing operations.

#### 4. Targeting Patterns

- **Sector focus:** Scattered Spider has consistently targeted sectors like financial services, retail, entertainment, telecommunications, cloud storage platforms, and software providers.
- **Domain keyword usage:** Their phishing domains often include words mimicking enterprise or IT support services—such as “connect,” “corp,” “duo,” “help,” “he1p,” “it,” “mfa,” “okta,” “servicedesk,” “support,” “vpn,” and “workspace”—frequently using top-level domains like .com, .co, .us, .net, .org, and .help to enhance credibility and social engineering effectiveness.

#### 5. Behavioral Traits

- **Rapid infrastructure adaptation:** The group swiftly rotates domains and adapts hosting setups to avoid blacklistings and takedowns.
- **On-page and server content manipulation:** They regularly update HTML, JavaScript, and deployment processes to evade detection signatures and improve phishing realism.

---

---

## 2024 Arrests Linked to Scattered Spider

Throughout 2024, law enforcement made several major arrests and charges against members and alleged leaders of the Scattered Spider (aka 0ktapus, UNC3944, etc.) cybercriminal group. Here’s a chronological summary of these notable actions:

## January 2024

- **Noah Michael Urban** (aliases: “Sosa,” “King Bob,” “Elijah”) was arrested in Florida. Urban was implicated in SIM swapping schemes that led to the theft of approximately $800,000 in cryptocurrency. He is considered a key suspect in Scattered Spider’s activities.

## June 2024

- **Tyler Buchanan** (alias: “TylerB”), believed to be an alleged leader of Scattered Spider, was arrested in Spain. At the time of his arrest, authorities seized $27million in Bitcoin.

## July 2024

- A 17-year-old from Walsall, West Midlands, UK, was apprehended by local law enforcement in collaboration with the FBI. The individual was reportedly connected to Scattered Spider’s operations.

## November 2024

![](image-14.png)

- **Five group members were charged by U.S. prosecutors**, following extensive international investigations. The indicted individuals included:
  - Tyler Buchanan, 22, of Scotland
  - Ahmed Elbadawy, 23, of College Station, TX
  - Joel Evans, 25, of Jacksonville, NC
  - Evans Osiebo, 20, of Dallas, TX
  - Noah Urban, 20, of Palm Coast, FL
- The charges detail the group’s involvement in complex hacking schemes targeting businesses and individuals.

## December 2024

- **Remington Goy Ogletree**, a 19-year-old from Fort Worth, TX, was arrested after the FBI organized a sting operation. Ogletree was lured into a fake cryptocurrency laundering setup dubbed “Cash Service,” which led to his capture for his role in telecom-related breaches.

---

---

**2025 Scattered Spider**

The new 2025 Scattered Spider **Phishing Kit #5** was identified following research by threat intel researcher **Lontz**, who published details on January 23, 2025, about new potential Scattered Spider infrastructure. This discovery enabled analysts to create a fingerprint for this latest phishing kit, marking the fifth unique version tracked since 2023.

![](image-15.png)
![](image-16-1024x553.png)
![](image-17-1024x538.png)

---

![](image-18-1024x492.png)

---

---

- **Additional domains identified using this kit include:**
  - corp-hubspot[.]com (targeting HubSpot)
  - morningstar-okta[.]com (Morningstar)
  - pure-okta[.]com (Pure Storage)
  - signin-nydig[.]com (New York Digital Investment Group)
  - sso-instacart[.]com (Instacart)
  - sts-vodafone[.]com (Vodafone)

---

---

The web pages crafted from the 2025 Scattered Spider phishing kit were designed to closely mimic the targeted organization’s Okta portal. These pages prominently displayed the organization’s logo and name, alongside a “Powered by Okta” footer or header, enhancing their credibility and making the deception more convincing to victims. This precise replication of the Okta login experience was a key characteristic of phishing kits used by Scattered Spider in 2023 through 2025.  
  
The phishing kit used short-lived, brand-themed domains that often included keywords like “okta,” “sso,” “help,” and other IT-related terms to appear legitimate. These domains hosted phishing pages that appeared almost identical to genuine Okta login portals, making detection by users difficult. Once credentials were submitted, the phishing infrastructure would immediately exfiltrate the data for attacker use.

![](image-20.png)

---

Scattered Spider’s use of the Evilginx framework—a standalone man-in-the-middle (MitM) attack tool—is a sophisticated element in their phishing arsenal designed to hijack authentication sessions and capture credentials. Analysts have observed that across the group’s first three phishing kits, victims were often redirected to the Rick Astley YouTube video, a classic “Rick Roll” meme. This redirection serves as a method to obscure the malicious payloads delivered by Evilginx, demonstrating a layer of deception aiming to evade immediate suspicion.

Several domains linked to Scattered Spider have been identified as hosting Evilginx software. These domains show consistency with the group’s known domain registration and hosting behaviors:

**Domains hosting Evilginx:**

```
corp-azure[.]com

corporatetools-okta[.]com

hr-myccmortgage[.]com

hr-synovus[.]com

These domains were registered via registrars like Hosting Concepts, GoDaddy, and NiceNIC.

They were hosted on infrastructure providers including Virtuo, DigitalOcean, and Choopa.

Further investigation into the IP ranges hosting these domains uncovered additional domains exhibiting the same naming and infrastructure patterns:

Additional domains found through IP pivots:

7-eleven-hr[.]com

bell-hr[.]com

cts-comcast[.]com

doordash-support[.]com
```

![](image-21.png)

---

---

Since the second quarter of 2024, Scattered Spider has diversified and shifted its infrastructure preferences, notably renting dedicated servers from more privacy-focused hosting providers. These include Virtuo and Njalla, both recognized for their emphasis on anonymity and resistance to takedown requests. This change marks an evolution in Scattered Spider’s operational security, reflecting increased sophistication in avoiding detection and disruption.

Regarding their autonomous system number (ASN) and hosting provider usage timeline:

- **Hostinger** (**AS47583**) and **Vultr (AS20473)** were among the early providers used starting in September 2023.
- **BitLaunch** (**BL Networks, AS399629**) appeared in March 2024.
- **DigitalOcean (AS14061)** and an unknown provider via **railnet** (**AS214943**) were engaged in April 2024.
- **HostKey** (**AS57043**) came into use by June 2024.
- Later additions included GlobalData Cloud (**AS42624**) in July 2024, **Virtuo** Host (**AS399486**) in August 2024, and **Njalla** (**AS39287**) starting in October 2024.
- Notably, Cloudflare (AS13335), a major Internet services provider known for CDN and security services, came into play in January 2025, marking a new trend for Scattered Spider.

The preferred domain registrar since the second quarter of 2024 has been **NiceNIC**, which aligns with many of the domains registered thereafter.

The last observed usage of Virtuo as a hosting provider was in October 2024, while **Njalla** was last used in November 2024. As of January 2025, Scattered Spider incorporated Cloudflare services into their hosting infrastructure, indicating an expansion into using mainstream yet robust platforms alongside privacy-centric hosts.

---

---

A new Telegram channel called “Scattered LAPSUS$ Hunters” emerged in early August 2025, blending the personas, tactics, and threat actor profiles of three known groups: Scattered Spider (UNC3944), LAPSUS$, and ShinyHunters. This channel has rapidly posted a chaotic mix of alleged breaches, ransom threats, political provocations, and boasts of a large, yet unverified, exploit arsenal.

Key highlights and timeline of activity on this channel include:

- **August 8, 2025 – Channel Launch & Initial Leaks:**
  - Claims of breaches affecting luxury brands such as Gucci (100 customer records), Chanel (Salesforce campaign breach), Neiman Marcus (database for sale at 1 BTC), and Coca-Cola Europacific Partners (vendor contact list).
  - Threats issued against U.S. Department of Homeland Security (DHS), UK’s National Crime Agency, and governments of England, France, Brazil, and India.
  - Political taunts targeting Israeli Prime Minister Netanyahu and Iran’s IRGC.
  - Mockery of cybersecurity firm CrowdStrike under the nickname “CrowdShart.”
  - A Telegram poll led to the public release of Coca-Cola vendor contact data, considered low operational risk but valuable for open-source intelligence (OSINT).
- **August 9, 2025 – Escalating Threats and Claims:**
  - Issuance of a hostage-style ultimatum to the UK Ministry of Justice demanding the release of an arrested member named “Jared Antwon” or the threat to leak sensitive GitHub repositories and the Legal Aid Agency database.
  - Alleged breach of Banco Santander exposing 30 million customer records, including 6 million account balances and 28 million credit card records, priced at about 30 BTC (~$1.7M).
  - Threats against Zomato.com framed as “punishment” with promised shell access release contingent on social media reactions.
  - Showcasing luxury items allegedly purchased with ransom money from AT&T, with disclaimers distancing from ransomware affiliation.
  - Announcements of impending “massive leaks” targeting Cartier and Louis Vuitton, aiming to induce panic within high-end retail sectors.
- **August 10, 2025 – Technical Claims and Exploit Arsenal:**
  - Taunts targeting Splunk following access blocks due to U.S. export restrictions, with claims of possessing a Splunk zero-day vulnerability available for sale or use.
  - Presentation of a large list of alleged zero-day (0day), one-day (1day), and future vulnerabilities covering a wide range of platforms and applications, including iOS, Android (Samsung Messenger), major browsers (Firefox, Safari, Chrome, Tor), Windows and Linux privilege escalations, network devices (Fortinet, SonicWall, Juniper), VMware, Adobe Reader, and Microsoft Word. These claims remain unverified with no proof-of-concept or exploit code released.

While much of the data and exploit claims have not been independently verified, some posted data dumps—such as those from Gucci, Neiman Marcus, Chanel, Coca-Cola, and Banco Santander—have been validated as genuine but vary in criticality. The channel exhibits a noisy, disjointed style mixing real breaches, extortion tactics, political messaging, and boastful claims, reflecting a fusion of the distinct characteristics and online presence of Scattered Spider, LAPSUS$, and ShinyHunters.

![](image-22-1024x580.png)

---

---

## MITRE Table

|  |  |
| --- | --- |
| [T-Code](https://attack.mitre.org/groups/G1015/) | Description |
| T1087 | Account discovery |
| T1098 | Account Manipulation |
| T1217 | Browser Information Discovery |
| T1580 | Cloud Infrastructure Discovery |
| T1538 | Cloud Service Dashboard |
| T1136 | Create Account |
| T1486 | Data Encrypted for Impact |
| T1530 | Data from Cloud Storage |
| T1213 | Data from Information Repositories |
| T1074 | Data Staged |
| T1006 | Direct Volume Access |
| T1484 | Domain or Tenant Policy Modification |
| T1114 | Email Collection |
| T1567 | Exfiltration Over Web Service |
| T1190 | Exploit Public Facing Application |
| T1068 | Exploitation for Privilege Escalation |
| T1133 | External Remote Services |
| T1083 | File and Directory Discovery |
| T1657 | Financial Theft |
| T1589 | Gather Victim Identity Information |
| T1564 | Hide Artifacts |
| T1656 | Impersonation |
| T1105 | Ingress Tool Transfer |
| T1556 | Modify Authentication Process |
| T1578 | Modify Cloud Compute Infrastructure |
| T1621 | Multi-Factor Authentication Request Generation |
| T1046 | Network Service Discovery |
| T1588 | Obtain Capabilities: Tool |
| T1003 | OS Credential Dumping |
| T1069 | Permission Groups Discovery: Cloud Groups |
| T1566 | Phishing: Spearphishing Voice |
| T1598 | Phishing for Information |
| T1572 | Protocol Tunneling |
| T1090 | Proxy |
| T1219 | Remote Access Tools |
| T1021 | Remote Services: Cloud Services |
| T1018 | Remote System Discovery |
| T1539 | Steal Web Session Cookies |
| T1553 | Subvert Trust Controls: Code Signing |
| T1552 | Unsecured Credentials |
| T1078 | Valid Accounts |
| T1102 | Web Service |
| T1047 | Windows Management Instrumentation |
| T1660 | Phishing |
| T1451 | Sim Swapping |

---

---

**IOCs**

- 7-eleven-hr[.]com
- activecampiagn[.]net
- acwa-apple[.]com
- bbtplus[.]com
- bell-hr[.]com
- bestbuy-cdn[.]com
- birdsso[.]com
- citrix-okta[.]com
- commonspiritcorp-okta[.]com
- consensys-okta[.]com
- corp-hubspot[.]com
- cts-comcast[.]com
- doordash-support[.]com
- duelbits-cdn[.]com
- freshworks-hr[.]com
- gemini-sso[.]com
- gucci-cdn[.]com
- itbit-okta[.]com
- iyft[.]net
- klaviyo-hr[.]com
- login.freshworks-hr[.]com
- login.hr-intercom[.]com
- morningstar-okta[.]com
- mytsl[.]net
- okta-ziffdavis[.]com
- pfchangs-support[.]com
- prntsrc[.]net
- pure-okta[.]com
- signin-nydig[.]com
- simpletexting-cdn[.]com
- squarespacehr[.]com
- sytemstern[.]net
- sso-instacart[.]com
- sts-vodafone[.]com
- twitter-okta[.]com
- xn--gryscale-ox0d[.]com
- x-sso[.]com

---

---

## Conclusion

The emergence of the **“Scattered LAPSUS$ Hunters”** Telegram channel highlights how today’s threat landscape is increasingly defined by **blended threat actor personas**, weaponized publicity, and rapid escalation tactics. Whether this group is a direct offshoot of Scattered Spider, an opportunistic alliance, or simply individuals mimicking multiple established crews, their blend of **validated breaches**, **unverified high-impact claims**, **political posturing**, and **attention-grabbing theatrics** makes them unpredictable and potentially dangerous.

While much of their purported exploit arsenal remains unconfirmed, the group’s ability to **quickly leak genuine data** and target high-value sectors—combined with their loud and chaotic online presence—closely mirrors the psychological pressure campaigns of both **LAPSUS$** and **ShinyHunters**, alongside the **precision social engineering** of Scattered Spider.

For defenders, this serves as a reminder that modern cyber threats often **blur the lines between traditional cybercrime operations, hacktivism, and digital extortion**. The overlap of tactics, techniques, and personas can complicate attribution and accelerate the potential for reputational and operational damage.

Organizations, especially in **luxury retail, financial services, and government**, should prioritize:

- Continuous monitoring for mentions in threat actor channels
- Strengthened identity and access verification processes
- Incident response playbooks that account for both **verified breaches** and **psychological pressure campaigns**

In the end, whether the “Scattered LAPSUS$ Hunters” are the next evolution of an existing crew or a short-lived publicity stunt, their activity underscores the **need for proactive intelligence, rapid verification of claims, and resilience planning** in the face of an increasingly theatrical and unpredictable cyber threat environment.
