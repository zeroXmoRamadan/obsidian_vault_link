# THM — SOC Fundamentals

> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #soc #blue-team #fundamentals #defensive-security

---

## Overview

Covers the core concepts of a Security Operations Center — what it is, what it detects, who works in it, how they operate, and what tools they use. Ends with a hands-on Level 1 analyst lab.

---

## Task 1 — What is a SOC?

- **SOC** = **Security Operations Center**
- A dedicated facility run by a specialized security team
- Goal: **continuously monitor** an organization's network and resources, detect suspicious activity, and prevent damage
- Operates **24/7**

---

## Task 2 — Detection & Response + The Three Pillars

### Detection Capabilities

|Capability|Description|
|---|---|
|**Detect Vulnerabilities**|Identify unpatched weaknesses in systems/software|
|**Detect Unauthorized Activity**|Spot credential abuse, anomalous logins (e.g. geo-location flags)|
|**Detect Policy Violations**|Pirated software, insecure file transfers, etc.|
|**Detect Intrusions**|Unauthorized access via exploited apps or malware infection|

### Response Capability

- **Support incident response** — minimize impact, assist with root cause analysis

### The Three Pillars of a SOC

> **People → Process → Technology**

All three must coexist for a mature, effective SOC.

---

## Task 3 — People (The SOC Team)

Human analysts are essential — security tools generate noise, and people are needed to distinguish real threats from false positives.

|Role|Responsibilities|
|---|---|
|**L1 Analyst**|First responder; basic alert triage and reporting|
|**L2 Analyst**|Deeper investigation; correlates data across multiple sources|
|**L3 Analyst**|Proactive threat hunting; leads containment, eradication, recovery|
|**Security Engineer**|Deploys and configures security solutions|
|**Detection Engineer**|Builds detection rules and alert logic|
|**Manager**|Oversees processes; reports to CISO on security posture|

> **Note:** Team size and roles scale with the organization's size and risk profile.

---

## Task 4 — Processes

### Alert Triage — The 5 Ws

Every alert is analyzed by answering:

|W|Question|Example Answer|
|---|---|---|
|**What?**|What activity was detected?|Malicious file detected|
|**When?**|When did it occur?|13:20, June 5, 2024|
|**Where?**|Where was it detected?|Host: GEORGE_PC, Downloads folder|
|**Who?**|Who was involved?|User: George|
|**Why?**|What was the intent/cause?|Downloaded pirated software|

### Reporting

- Harmful alerts are **escalated as tickets** to higher-level analysts
- Reports must include all 5 Ws, thorough analysis, and **screenshots as evidence**

### Incident Response & Forensics

- Critical detections trigger a formal **Incident Response** process
- Forensic analysis may follow to determine **root cause** from system/network artifacts

---

## Task 5 — Technology (Security Solutions)

|Tool|Function|Detection or Response?|
|---|---|---|
|**SIEM** (Security Information & Event Management)|Collects logs from all sources; correlates events against detection rules; modern versions add UEBA and threat intel|Detection only|
|**EDR** (Endpoint Detection & Response)|Real-time and historical visibility into endpoint activity; supports automated response|Both|
|**Firewall**|Monitors and filters incoming/outgoing network traffic; blocks unauthorized connections|Both|

> Other tools in a SOC ecosystem: **Antivirus, IDS/IPS, XDR, SOAR**, and more. Tool selection depends on the organization's threat surface and resources.

---

## Task 6 — Practical Lab (Level 1 Analyst Scenario)

**Scenario:** Port scanning activity detected on an internal host. Investigate via SIEM logs and answer the 5 Ws.

> **Note:** The SOC team confirmed the scan originated from `10.0.0.8` as an authorized internal test.

|5W|Answer|
|---|---|
|**What** — Activity that triggered the alert?|_(found in lab)_|
|**When** — Time of the activity?|_(found in lab)_|
|**Where** — Destination host IP?|_(found in lab)_|
|**Who** — Source host name?|_(found in lab)_|
|**Why** — Intended or malicious?|_(found in lab)_|
|**Extra** — Was any response sent back to the scanner IP?|_(yea/nay — found in lab)_|
|**Flag** after closing the alert?|_(found in lab)_|

---

## Key Takeaways

- The SOC's core mission is **Detection + Response**, operating around the clock
- No single pillar is enough — mature SOCs need skilled **People**, solid **Processes**, and the right **Technology**
- Alert triage using the **5 Ws** is the foundation of an analyst's daily workflow
- Tools like **SIEM** centralize detection; **EDR** and **Firewalls** add response capability
- L1 analysts are the entry point — triage, report, escalate

---

## Related Notes

- [[Junior Security Analyst Intro]]
- [[Alert Triage Process]]
- [[Incident Response Basics]]
- [[SIEM Fundamentals]]
- [[TryHackMe SOC Level 1 Path]]