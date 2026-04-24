> **Platform:** TryHackMe  
> **Path:** SOC Level 1 / Pre-Security  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #blue-team #defensive-security #soc #intro

---

## Overview

A broad introduction to defensive security (blue teaming) — what it covers, who does it, what tools are used, and why it matters. Includes a hands-on SIEM investigation scenario at FakeBank.

---

## Task 1 — Why Defensive Security Matters

Real-world breaches demonstrate the cost of poor security:

|Organisation|Year|Impact|Fine|
|---|---|---|---|
|**British Airways**|2018|400,000+ customers' personal & payment data leaked|£20 million|
|**Marriott International**|2020|334 million customers' passport & payment data leaked (outdated systems)|$52 million|
|**Advanced Computer Software Group**|2022|Medical records & phone numbers of ~80,000 people leaked|£3.07 million|
|**23andMe**|2023|7 million+ users' names, addresses, health & DNA data leaked|£2.31 million|
|**SK Telecom**|2024|~27 million users' data leaked via misconfigured servers|$97 million|

What is defensive security also known as?
- Blue Teaming

---

## Task 2 — Key Areas of Defensive Security

|Area|Description|
|---|---|
|**Monitoring & Detection**|Continuously observe network/system activity for suspicious behaviour (e.g. login from unexpected country)|
|**Incident Response**|Contain and remove confirmed threats; restore normal operations|
|**Threat Intelligence**|Gather info on attacker methods, targets, and trends to strengthen defences proactively|
|**Vulnerability Management**|Identify and patch software/system flaws before attackers can exploit them|
|**Investigation & Analysis**|Separate normal from suspicious activity; dig into details to uncover insights|

### Key Roles in a Defensive Security Team

| Person      | Role               | Responsibilities                                                                   |
| ----------- | ------------------ | ---------------------------------------------------------------------------------- |
| **Bob**     | Analyst            | Monitors network/system events; frontline threat detection                         |
| **Aaliyah** | Incident Responder | Investigates and responds to active incidents in real time; shares lessons learned |
| **Zoe**     | Security Engineer  | Builds and maintains tools and systems that support the team                       |
| **Bill**    | Digital Forensics  | Gathers, preserves, and analyses evidence to understand what happened and how      |

An attack has been detected on an organisation's network. What is the name of the person above who would be responsible for responding to the attack?
- Aaliyah

---

## Task 3 — Defence in Depth & Key Technologies

Organisations layer multiple defences so that if one fails, others remain. This is called **Defence in Depth**.

### Defensive Measures

|Measure|Purpose|
|---|---|
|**Employee Training**|Teach staff to recognise phishing and social engineering attempts|
|**IDS** (Intrusion Detection Systems)|Monitor network/systems and alert on suspicious activity|
|**Firewalls**|Control what traffic enters or leaves the network|
|**Security Policies**|Enforce rules like strong passwords, website blocking, access controls|

### Key Technologies

**SOC (Security Operations Center)**

- The defensive "nerve centre" of an organisation
- Operates 24/7, 365 days a year
- Daily tasks: reviewing alerts, investigating anomalies, responding to incidents

**SIEM (Security Information & Event Management)**

- Centralises logs and data from all devices across the organisation (servers, workstations, firewalls, etc.)
- Acts like a radar — sweeps the environment and surfaces suspicious events
- Enables multiple analysts to review and act on data quickly from one place

What is the abbreviation for the term "Security Operations Centre"?
- SOC

---

## Task 4 — Practical Lab (FakeBank SIEM Investigation)

**Scenario:** Junior analyst at FakeBank investigating a **Web Discovery Attack** flagged by the SIEM.

1. 

|Question|Answer|
|---|---|
|Flag after securing FakeBank?|`THM{FAKEBANK-SECURED}`|

---

## Key Takeaways

- Defensive security protects organisations from attacks that can cost **millions in fines** and reputational damage
- Blue teams operate across five key areas: monitoring, incident response, threat intel, vulnerability management, and investigation
- **Defence in Depth** means layering tools and policies so no single failure is catastrophic
- The **SOC** is the operational hub; the **SIEM** is its most critical tool for centralising visibility
- Analyst, incident responder, engineer, and forensics are all distinct but complementary roles

---

## Related Notes

- [[SOC Fundamentals]]
- [[SOC Role in Blue Team]]
- [[Junior Security Analyst Intro]]
- [[Alert Triage Process]]
- [[SIEM Fundamentals]]
- [[TryHackMe SOC Level 1 Path]]