> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #vulnerabilities #misconfigurations #supply-chain #blue-team #soc

---

## Overview

Explores how systems (servers, VMs, cloud platforms) are targeted by threat actors — through human error, software vulnerabilities, misconfigurations, and supply chain attacks — and how SOC analysts respond.

---

## Task 2 — Why Systems Are Valuable Targets

A system is any platform storing or processing data — physical servers, virtual machines, or cloud services like Microsoft 365. Breaching a system is far more impactful than breaching a single user.

|Breached System|Attack Value|
|---|---|
|School student's laptop|Steal Steam profile; add PC to a botnet|
|Bank IT admin's laptop|Access internal banking systems|
|Criminal law firm's mail server|Dump all mailboxes and blackmail the firm|
|Industrial network server|Encrypt the whole network with ransomware|
|Government website panel|Deface or destroy website content (hacktivism)|

Can cyber attacks happen without victim intervention (Yea/Nay)?
- Yea
  
Can a breach of just a single system lead to disastrous consequences (Yea/Nay)?
- Yea

---

## Task 3 — How Systems Are Attacked

### Human-Led Attacks

Users are often the entry point — inserting a found USB, downloading pirated software, or reusing weak passwords.

> **81%** of breaches involve stolen or weak passwords.

### Software Vulnerabilities

Every piece of software can have security flaws. In 2024 alone:

- **40,000+** software vulnerabilities were published
- **300+** were actively exploited in major attacks

IT admins also increase risk by using weak passwords or allowing unrestricted system access.

### Supply Chain Attacks

Attackers compromise a widely-used app or library and push a malicious update to all users — affecting thousands of organisations at once.

|Example|Impact|
|---|---|
|**SolarWinds**|Thousands of companies compromised via a trojanised software update|
|**3CX**|Phone software supply chain breach affecting global businesses|
|**Lottie Player** (TryHackMe)|Animation library compromised — even THM was affected|

> Supply chain attacks are hard to defend against because you can't always control every library or app on your systems.

What is the term for a security flaw that can be exploited to breach a system?
- Vulnerability

What is the name of the attack when malware comes from a trusted app or library?
- Supply Chain

---

## Task 4 — Software Vulnerabilities Deep Dive

- Vulnerabilities can exist for years before discovery — **Shellshock** (1992) wasn't found until **2014**
- **Zero-day** — a vulnerability discovered and exploited by attackers _before_ anyone else knows it exists
- Once made public, a vulnerability is assigned a **CVE** (Common Vulnerabilities and Exposures) number
- From that point it's a race: attackers build exploits while defenders patch


![](678ecc92c80aa206339f0f23-1752598.png)

### Responding to Vulnerabilities

|Response|Description|
|---|---|
|**Apply the patch**|Always the primary fix — update supplied by the software vendor|
|**Restrict access**|Limit system access to trusted IPs/users while waiting for a patch|
|**Temporary vendor measures**|Apply any interim workarounds provided by the vendor|
|**Block known patterns**|Use IDS/IPS or WAF to block known exploit signatures|

What is the CVE for the critical SharePoint vulnerability dubbed "ToolShell"?
- CVE-2025-53770

How would you respond to a detected vulnerability on your system?
- Patch

---

## Task 5 — Misconfigurations

A misconfiguration is not a software bug — it's a human setup mistake, often made to simplify things.

![](678ecc92c80aa206339f0f23-1754915.png)

### Real-World Examples

|Case|Result|
|---|---|
|Password "123456" on McDonald's recruitment system|Exposed chats for **64 million** job applications|
|Misconfigured cloud storage|Breached **106 million** bank customers' data|
|Improperly configured smart fridges|Silently recruited into large-scale botnet attacks|

### Responding to Misconfigurations

|Measure|Description|
|---|---|
|**Penetration Testing**|Hire ethical hackers to simulate attacks and report discovered flaws|
|**Vulnerability Scans**|Periodically run tools to detect default passwords and outdated software|
|**Configuration Audits**|Manually review systems against security benchmarks (e.g. CIS benchmarks)|

Can a system patch or software update fix the misconfigurations (Yea/Nay)?
- Nay

Which activity involves an authorized cyber attack to detect the misconfigurations?
- Penetration Testing

---

## Task 6 — Mitigation Measures for Systems

Unlike humans, systems can't be _trained_ — but IT teams can be. Key mitigations:

![](678ecc92c80aa206339f0f23-1752599.png)

|Measure|Description|
|---|---|
|**Patch Management**|Track and apply patches promptly to reduce exploitation windows|
|**IT Training**|Educate IT teams on misconfiguration risks and secure setup practices|
|**Network Protection**|Restrict system access to trusted users or IP addresses|
|**Antivirus Protection**|Detect and stop many attacks at the endpoint level|

### Lab — TryHackMe Security Dashboard

#### 1. Systems at Risk
1. ![](Pasted%20image%2020260425014240.png)
2. ![](Pasted%20image%2020260425014246.png)
3. ![](Pasted%20image%2020260425014250.png)
4. ![](Pasted%20image%2020260425014254.png)
![](Pasted%20image%2020260425014256.png)

#### 2. Remediation Plan


| Challenge        | Flag                          |
| ---------------- | ----------------------------- |
| Systems at Risk  | _THM{patch_or_reconfigure?}_  |
| Remediation Plan | _THM{best_systems_defender!}_ |

---

## Key Takeaways

- Breaching a **system** is far more impactful than breaching a single user account
- Attacks come via humans, software vulnerabilities, misconfigurations, and supply chains
- **Zero-days** are the hardest to defend — vigilant monitoring is the only option until a patch arrives
- **CVE numbers** track public vulnerabilities — patching speed is critical once published
- Misconfigurations are common, avoidable, and often only discovered _after_ exploitation
- Supply chain attacks bypass perimeter defences — SOC analysts must be ready to respond

---

## Threat Intel Resources

|Resource|URL|
|---|---|
|Verizon DBIR: How Real Intrusions Happen|https://www.verizon.com/business/resources/reports/dbir|
|CISA: Known Exploited Vulnerabilities Catalog|https://www.cisa.gov/known-exploited-vulnerabilities-catalog|
|BleepingComputer: Supply Chain Attacks|https://www.bleepingcomputer.com|
|CheckPoint: Live Cyber Threat Map|https://threatmap.checkpoint.com|
