> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #alert-triage #soc #blue-team #l1-analyst #incident-response

---

## Overview

Covers the full lifecycle of a security alert — from how events become alerts, to how L1 analysts prioritise, investigate, and close them. An essential foundation before tackling the SOC Simulator and SAL1 certification.

---

## Task 2 — From Events to Alerts

A raw event (login, file download, process launch) gets logged by a system, shipped to a SIEM or XDR, and — when it matches a detection rule — becomes an **alert**. Analysts triage dozens of alerts per day instead of reviewing millions of raw logs.

### Alert Management Platforms

| Solution | Examples | Description |
|---|---|---|
| **SIEM** | Elastic, Splunk | Solid alert management, ideal for most teams |
| **EDR / NDR** | MS Defender, CrowdStrike | Own dashboards, but prefer routing to SIEM |
| **SOAR** | Splunk SOAR, Cortex | Aggregates alerts from multiple solutions |
| **Ticketing** | Jira, TheHive | Custom ticket-based alert workflow |

### L1 Role in Alert Triage

| Role | Responsibility |
|---|---|
| **L1 Analyst** | Review alerts, distinguish real threats from noise, escalate to L2 |
| **L2 Analyst** | Receive escalations, perform deeper analysis and remediation |
| **SOC Engineer** | Ensure alerts contain enough data for efficient triage |
| **SOC Manager** | Track triage speed and quality to prevent missed attacks |

What is the number of alerts you see in the [SOC dashboard (opens in new tab)]?
![](Pasted%20image%2020260501152844.png)
- 5

What is the name of the most recent alert you see?
- Double-Extension File Creation

---

## Task 3 — Alert Properties

Every alert, regardless of platform, shares a common set of fields.

| # | Property | Description | Examples |
|---|---|---|---|
| 1 | **Alert Time** | When the alert was created — usually a few minutes after the actual event | Alert: 15:35 / Event: 15:32 |
| 2 | **Alert Name** | Summary of what happened, based on the detection rule | Unusual Login Location, Mimikatz Usage |
| 3 | **Alert Severity** | Urgency level set by detection engineers; can be adjusted | 🟢 Low → 🔴 Critical |
| 4 | **Alert Status** | Whether someone is working it or it's resolved | 🆕 New → 🔄 In Progress → ✅ Closed |
| 5 | **Alert Verdict** | Classification — is it a real threat or noise? | 🔴 True Positive / 🟢 False Positive |
| 6 | **Alert Assignee** | Analyst who owns the alert and is responsible for it | Also called alert owner |
| 7 | **Alert Description** | Explains the rule logic, why it signals an attack, and triage hints | Three-section layout in most platforms |
| 8 | **Alert Fields** | Raw values that triggered the alert | Affected hostname, commandline entered, etc. |

What was the verdict for the "Unusual VPN Login Location" alert?
![](Pasted%20image%2020260501152934.png)
- False Positive

What user was mentioned in the "Unusual VPN Login Location" alert?
![](Pasted%20image%2020260501153000.png)
- M.Clark

---

## Task 4 — Alert Prioritisation

With many alerts in the queue, order matters. The standard approach:

1. **Filter** — Only take `New` alerts not already assigned or in progress
2. **Sort by Severity** — Critical → High → Medium → Low  
   *(Critical alerts are statistically more likely to be real, major threats)*
3. **Sort by Time** — Oldest first  
   *(An older breach means the attacker has had more time inside the network)*

Should you first prioritise medium over low severity alerts? (Yea/Nay)
- Yea

Should you first take the newest alerts and then the older ones? (Yea/Nay)
- Nay

Assign yourself to the first-priority alert and change its status to **In Progress**.  
The name of your selected alert will be the answer to the question.
![](Pasted%20image%2020260501153053.png)
- Potential Data Exfiltration

---

## Task 5 — Alert Triage Workflow

> Also called: alert handling, alert processing, alert investigation, or alert analysis.

### Initial Actions
- Assign the alert to yourself
- Move status to **In Progress**
- Read the alert name, description, and key indicator fields

### Investigation
Some teams provide **Workbooks** (a.k.a. playbooks / runbooks) for specific alert categories. Without one, follow this structure:

1. Identify **who** is affected — user, hostname, cloud asset, or network segment
2. Identify **what** action occurred — suspicious login, malware execution, data exfil attempt
3. Review **surrounding events** — look for suspicious activity before or after the alert timestamp
4. Use **threat intelligence** platforms to validate your analysis

### Final Actions
- Decide: **True Positive** (real threat) or **False Positive** (noise)
- Write a detailed **comment** explaining your steps and verdict reasoning
- Move the alert to **Closed** status on the dashboard

> If you didn't receive a flag after triage, your verdict or fields were incorrect. Use **Restart** in the top-right of the TryHackMe VM to reset.


### Lab — TryHackMe SOC Dashboard
#### 1- Which flag did you receive after you correctly triaged the first-priority alert?
1. ![](Pasted%20image%2020260501153549.png)
2. ![](Pasted%20image%2020260501153615.png)
3. ![](Pasted%20image%2020260501153628.png)
#### 2- Which flag did you receive after you correctly triaged the second-priority alert?
1. ![](Pasted%20image%2020260501153720.png)
2. ![](Pasted%20image%2020260501153750.png)
3. ![](Pasted%20image%2020260501153753.png)
#### 3- Which flag did you receive after you correctly triaged the third-priority alert?
1. ![](Pasted%20image%2020260501153847.png)
2. ![](Pasted%20image%2020260501153912.png)
3. ![](Pasted%20image%2020260501153916.png)

| Challenge             | Flag                                    |
| --------------------- | --------------------------------------- |
| First-priority alert  | _THM{looks_like_lots_of_zoom_meetings}_ |
| Second-priority alert | _THM{how_could_this_user_fall_for_it?}_ |
| Third-priority alert  | _THM{how_could_this_user_fall_for_it?}_ |

---

## Key Takeaways

- Alerts exist to filter millions of raw logs down to dozens of actionable events for analysts
- L1 analysts are the **first line of defence** — their triage decisions determine whether an attack is caught or missed
- Prioritise by **severity first**, then by **time** (oldest critical alerts are the most urgent)
- The triage workflow: **Assign → Investigate → Classify → Comment → Close**
- A **True Positive** verdict alone doesn't stop an attack — escalation and L2 response follow
- **Workbooks** help standardise investigation steps for specific alert types