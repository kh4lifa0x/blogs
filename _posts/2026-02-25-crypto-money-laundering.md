---
title: "Crypto Money Laundering"
date: 2026-02-25 10:59:36 +0200
categories: [Threat Intelligence]
tags: [investigation, kimsuky, threat-actors]
image:
  path: DarkAtlas-Cryptpo-money-laundring-web-banner-v2.jpg-scaled.jpeg
  alt: "Crypto Money Laundering"
media_subpath: /assets/img/posts/crypto-money-laundering
toc: true
---

# Crypto Money Laundering: Definition, Stages, and Common Techniques

**Money laundering** is the process of **concealing illegally obtained funds** to make them appear legitimate. In crypto, laundering has evolved because digital assets can move quickly across borders and between platforms, often with limited identity context unless strong compliance controls are in place.

Crypto doesn’t make laundering invisible—blockchains are transparent—but it can make attribution harder due to **pseudonymous wallets**, **cross-chain movement**, and the use of services designed to obscure transaction trails.

## Why cryptocurrency is used for money laundering

Crypto laundering typically becomes easier when criminals exploit a combination of:

- **Pseudonymity:** Wallet addresses are public, but they aren’t automatically linked to a real-world identity.
- **Borderless transfers:** Assets can move globally in minutes, sometimes outside traditional banking rails.
- **Platform fragmentation:** Funds can be moved across exchanges, peer-to-peer platforms, and bridges—creating investigation complexity.
- **Obfuscation tools:** Mixers, chain-hopping, and privacy-enhancing methods can reduce traceability.

---

## The 3 stages of crypto money laundering

Crypto laundering often follows the same classic model: **placement → layering → integration**, but uses crypto-specific methods during each step.

### 1) Placement: introducing illicit value into crypto

This is the point where criminals move illicit funds into the crypto ecosystem. Common methods include:

- buying crypto with illicit cash through informal brokers
- receiving proceeds directly in crypto (fraud, ransomware, scams)
- converting stolen funds into crypto through compromised accounts

At this stage, the goal is to **get value into wallets and services** that allow further movement.

---

### 2) Layering: obscuring the audit trail

Layering is where crypto laundering becomes most complex. The goal is to **break the link** between the source and destination through multiple transactions and intermediaries.

Common layering techniques:

- **Mixers/tumblers:** pool funds and redistribute them to complicate tracing.
- **Chain-hopping:** swap between assets (e.g., BTC → ETH → other tokens) and networks to fragment the trail.
- **Cross-chain bridges:** move assets between chains, increasing the effort needed to follow flows.
- **Peeling chains:** repeated small transfers across many addresses to reduce clarity.

This stage often includes transfers into **high-volume venues** (centralized exchanges or P2P markets), where commingling can make analysis harder especially when transaction monitoring and identity verification are weak.

### 3) Integration: converting back to “usable” value

In the integration stage, criminals attempt to reintroduce “cleaned” value into the economy by:

- converting crypto to fiat (cash-out through exchanges or OTC channels)
- purchasing goods/services
- routing proceeds through “legitimate-looking” transactions

---

## The Broader Context

Cryptocurrency money laundering is sophisticated because it exploits both the transparency and pseudonymity of blockchain systems. While every transaction is permanently recorded, identifying the real-world actor behind a wallet address remains a significant challenge without additional intelligence or regulatory intervention.

Over the past decade, regulators and private-sector firms have developed blockchain analytics and compliance mechanisms to detect suspicious activity. However, as detection capabilities improve, laundering techniques continue to evolve—creating an ongoing challenge for law enforcement and financial institutions alike.

---

## Key laundering techniques explained

## Mixers (tumbling services)

Mixers are designed to **obscure transaction history** by pooling funds from many users, then redistributing them to new addresses—often in multiple rounds. This can make it harder to tie a specific input transaction to a specific output transaction.

![](image-1024x560.jpg)

---

## Chain-Hopping

Chain-hopping is the practice of rapidly moving value across different assets and networks using exchanges, decentralized swaps, or bridges to create a fragmented trail that investigators must reconstruct across multiple ledgers.

![](image-20-1024x683.png)

---

## How Actors Leverage Non-Compliant Crypto Exchanges

Non-compliant or weakly regulated exchanges are attractive because they may have:

- weak **KYC (Know Your Customer)** onboarding
- limited **AML (Anti-Money Laundering)** monitoring
- inconsistent enforcement across jurisdictions

Common exploitation patterns include:

**Weak KYC:** open accounts with minimal verification to reduce attribution.

**Commingling on deposit addresses:** funds mix with other user flows, complicating source tracing.

**Mixers + exchange cash-out:** use mixing before/after exchange deposits to weaken traceability.

**Dark Web Integration:**  
Some non-compliant exchanges may have ties to illicit marketplaces and networks. In these environments, cryptocurrency can be used to purchase illicit goods/services, and in some cases, to access laundering tools designed to obscure transaction trails.

![](image-21-1024x451.png)

---

## Real-world example: laundering after a major crypto heist [(Bybit)](https://www.ic3.gov/psa/2025/psa250226#:~:text=The%20Federal%20Bureau%20of%20Investigation,cyber%20activity%20as%20%22TraderTraitor.%22)

On **February 21, 2025**, Bybit suffered a theft of approximately **$1.5 billion in virtual assets**. The FBI attributed the theft to North Korea and referred to the activity as **“TraderTraitor.”** The FBI warned that the stolen assets were being converted and dispersed in an attempt to launder them into fiat.

This type of case illustrates a recurring pattern: after a large theft, actors often try to **move funds rapidly** across many addresses and services to complicate tracing and enforcement actions.

### How the Attack Happened

Investigators found that the attackers exploited a **software supply chain vulnerability** in a third-party multi-signature wallet provider used by Bybit—**Safe{Wallet}**. A developer’s machine was compromised, allowing malicious JavaScript to be injected into the wallet infrastructure. This enabled the hackers to manipulate a routine multisig transfer and **redirect funds from Bybit’s cold wallet to addresses under their control**.

### Theft and Laundering Tactics

Once the assets were transferred out, the attackers quickly moved the stolen funds across numerous wallets and blockchains in an effort to disguise their origin. Analysts observed that they used mixers, cross-chain bridges, and decentralized swap platforms—converting large amounts of Ethereum into other assets such as Bitcoin—to make tracing more difficult. A **portion of the stolen crypto became untraceable** due to these obfuscation techniques.

### Aftermath and Response

- **Funds Recovery Efforts:** Bybit launched a **bounty program** offering substantial rewards to anyone who could help trace or freeze the stolen assets—a move that generated significant community interest.
- **Partial Laundering:** Reports indicate that a significant amount (e.g., hundreds of millions of dollars) had been laundered or converted into other assets shortly after the hack.
- **Industry Impact:** The incident triggered broader concerns about exchange security and regulations, prompting reviews across the crypto sector.

![](image-23.png)

---

## [DPRK IT WORKERS](https://home.treasury.gov/news/press-releases/sb0190?utm_source)

**How the scheme works**

North Korean (DPRK) IT operatives have been reported to infiltrate global companies and generate income using their technical roles—often receiving payments in **cryptocurrency**. Those proceeds may then be moved through wallets and services in ways designed to reduce traceability, supporting broader state-linked financing activity.

### Enforcement and sanctions signals

In response, authorities have increased enforcement actions over recent years. Agencies such as the **U.S. Treasury’s Office of Foreign Assets Control (OFAC)** and South Korea’s **Ministry of Foreign Affairs (MOFA)** have imposed sanctions on individuals and entities connected to these operations. In many cases, sanctions listings reference **cryptocurrency addresses** as identifiers used to track and disrupt illicit financial activity.

### How investigators track these flows

Blockchain analytics providers (for example, Chainalysis) monitor DPRK-linked activity by tracking **sanctioned addresses**, compiling open-source intelligence, and mapping how funds move and consolidate. This work often focuses on patterns like routing through exchange accounts (including fictitious or proxy identities) and using over-the-counter (OTC) networks that may operate with limited oversight—highlighting the connection between state-sponsored cyber activity and crypto-enabled proliferation financing.

![](image-24.png)

---

## The Future of Crypto Money Laundering

The evolution of cryptocurrency has opened new avenues for financial innovation—but it has also created unprecedented opportunities for illicit activity. Crypto money laundering, fueled by the misuse of digital assets and the exploitation of non-compliant exchanges, has emerged as a pressing global challenge. Addressing this threat requires coordinated efforts across law enforcement, security agencies, and the private sector.

Over the past decade, significant progress has been made in financial intelligence and enforcement actions against money laundering. High-profile cases, such as Silk Road, demonstrate the capability of authorities to dismantle sophisticated criminal networks operating in the crypto space. Yet, the rapidly evolving nature of these crimes demands continuous vigilance, adaptive strategies, and technological innovation.

While the crypto laundering landscape presents complex challenges, it also offers opportunities to strengthen law enforcement and financial investigation capabilities. Success will depend on our ability to learn from emerging threats, adapt to new tactics, and collaborate across borders and industries to protect the integrity of global financial systems.

---

## Conclusion

Crypto-enabled money laundering remains an evolving threat to the global financial system. Criminals exploit pseudonymity, cross-chain movement, mixers, and weak compliance venues to obscure illicit proceeds. Reducing the risk requires consistent AML/KYC enforcement, cross-border cooperation, and strong investigative capabilities supported by timely disruption of laundering infrastructure.
