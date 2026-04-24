> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #soc #blue-team #career #structure

---

## Overview

Explores where the SOC sits within a company's broader security hierarchy, what other defensive teams exist, and how to navigate a career from L1 analyst onward.

**Prerequisites:** [[Junior Security Analyst Intro]], [[SOC Fundamentals]]

---

## Task 2 — Security Hierarchy


![[678ecc92c80aa206339f0f23-1756329.png]]

### Chain of Command

- **CEO / Executives** → focus on business objectives, not technical security
- **CISO** (Chief Information Security Officer) → hired to translate business needs into a security strategy and oversee all security departments

### Security Departments (in larger orgs)

|Team|Focus|
|---|---|
|**Red Team**|Offensive security — pentesters, ethical hackers finding vulnerabilities|
|**GRC Team**|Governance, Risk & Compliance — policies, regulations (e.g. GDPR, ISO 27001)|
|**Blue Team**|Defensive security — analysts, engineers, incident responders|

---

## Task 3 — Blue Team Structure

Blue Team = **defensive security**. Continuously monitors for attacks and responds quickly. Typical size: **3–50 members** depending on company size.

### Security Operations Center (SOC)

![[678ecc92c80aa206339f0f23-1756425.png]]

The most common entry point into cyber security. First line of defense, handles most alerts and attacks.

|Role|Responsibility|
|---|---|
|**L1 Analyst**|Triage alerts, escalate complex cases to L2|
|**L2 Analyst**|Investigate more advanced attacks|
|**SOC Engineer**|Configure and maintain security tools (SIEM, EDR, etc.)|
|**SOC Manager**|Manages the team and processes|

### Cyber Incident Response Team (CIRT)

![[678ecc92c80aa206339f0f23-1756425(1).png]]

Also called **CSIRT** or **CERT**. Called in when SOC expertise isn't enough or an incident escalates beyond control. Works without relying on standard SOC tools.

|Example|Scope|
|---|---|
|**JPCERT**|Japan's national CERT|
|**Mandiant**|Global private incident response firm|
|**CIRT (TryHackMe context)**|Investigates customer security incidents|

### Specialized Defensive Roles

![[678ecc92c80aa206339f0f23-1756425(2).png]]

Found in large enterprises, tech startups, and government agencies. Require deep expertise:

- **Digital Forensics Analyst** — Uncover hidden threats in disk and memory
- **Threat Intelligence Analyst** — Track emerging threat groups and TTPs
- **AppSec Engineer** — Secure software development lifecycle (SDLC)
- **Researcher** — Study threats and develop new defensive techniques

---

## Task 4 — SOC Career Path

### Getting Started as L1

1. Build core SOC skills (SIEM, alert triage, networking basics); red team and IT knowledge also helps
2. Practice via CTFs, follow cyber news, consider the **SAL1 certification**
3. Understand the **Internal vs MSSP** distinction, then apply
4. After gaining experience, progress to L2 or branch into a specialty

### Internal SOC vs MSSP

|Topic|Internal SOC|MSSP|
|---|---|---|
|**Scenario**|Protect one organization (e.g. a bank)|Protect dozens of clients across industries|
|**Working Pace**|Generally calmer, lower time pressure|High-pressure, queue of urgent alerts from shift start|
|**Security Tools**|Few tools, but deep expertise in each|Many diverse tools across all clients|
|**Incident Exposure**|Limited major incidents per year|Weekly exposure to breaches — fast learning|

> **Recommendation:** Apply for any open L1 position first. Both paths have value; MSSP accelerates experience.


![[678ecc92c80aa206339f0f23-1757446.png]]

### Possible Next Steps from L1

- **L2 Analyst** — most natural progression
- **SOC Engineer** — if tool configuration and automation appeals to you
- **CIRT** — if major incident response excites you
- **Management → CISO** — if leadership and strategy is your direction

---

## Task 5 — Final Challenge (CISO Simulation)

**Scenario:** As CISO of _TrySecureMe_, assign the right security roles to 7 simultaneous incidents using drag-and-drop.



| Question                             | Answer                         |
| ------------------------------------ | ------------------------------ |
| Flag after completing the challenge? | _THM{trysecureme_is_secured!}_ |

---

## Key Takeaways

- The **CISO** sits at the top of the security hierarchy, reporting to executive leadership
- **Blue Team** is the defensive counterpart to the Red Team — the SOC is its core unit
- The **CIRT** handles escalated or critical incidents that exceed normal SOC capacity
- Specialized roles (forensics, threat intel, AppSec) require broader experience first
- **Internal SOC** offers depth; **MSSP** offers breadth and faster incident exposure
- L1 is just the starting point — the path forward is wide open

---

## Related Notes

- [[Junior Security Analyst Intro]]
- [[SOC Fundamentals]]
- [[Incident Response Basics]]
- [[Humans as Attack Vectors]]
- [[Systems as Attack Vectors]]
- [[TryHackMe SOC Level 1 Path]]