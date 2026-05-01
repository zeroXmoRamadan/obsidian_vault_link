> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #alert-reporting #escalation #communication #soc #blue-team #l1-analyst

---

## Overview

Covers what happens after alert triage — how L1 analysts document findings, escalate real threats to L2, and communicate with other departments effectively.

---

## Task 2 — Reporting, Escalation & Communication

Most alerts are closed as False Positives or handled at L1 level. Complex or threatening ones move to L2. Three concepts enable that handoff:

![](678ecc92c80aa206339f0f23-1743606.png)

| Concept | Description |
|---|---|
| **Alert Reporting** | Document the investigation in detail before closing or escalating — especially critical for True Positives |
| **Alert Escalation** | Pass True Positive alerts requiring deeper action to L2, using the report as initial context |
| **Communication** | Contact other departments (IT, HR) during or after analysis for confirmation or additional info |

What is the process of passing suspicious alerts to an L2 analyst for review?
- Alert Escalation

What is the process of formally describing alert details and findings?
- Alert Reporting

---

## Task 3 — Why Reports Matter

| Purpose | Explanation |
|---|---|
| **Context for escalation** | Saves L2 time — they understand what happened without starting from scratch |
| **Permanent record** | Raw logs last 3–12 months; alerts are kept indefinitely — keep all context inside |
| **Skill development** | If you can't explain it simply, you don't understand it well enough |

![](678ecc92c80aa206339f0f23-1743611.png)

### Report Format — The 5 Ws

| W | What to Include |
|---|---|
| **Who** | Which user logged in, ran the command, or downloaded the file |
| **What** | The exact action or event sequence that occurred |
| **When** | When the suspicious activity started and ended |
| **Where** | Which device, IP address, or website was involved |
| **Why** | Your reasoning behind the final verdict — the most important W |

According to the SOC dashboard (opens in new tab), which user email leaked the sensitive document?

---

## Task 4 — When to Escalate

Escalate the alert to L2 if any of the following apply:

1. The alert indicates a **major cyberattack** requiring deeper investigation
2. **Remediation actions** are needed — malware removal, host isolation, password reset
3. **External communication** is required — customers, partners, management, law enforcement
4. You **don't fully understand** the alert and need senior support

### Escalation Steps

1. Move alert to **In Progress** and complete your analysis
2. Write the alert report and set your verdict
3. **Reassign** the alert to the L2 analyst on shift
4. Ping them in corporate chat or in person
5. L2 reads your report, validates the finding, and takes further action

> It's always better to escalate and discuss than to blindly close an alert you don't fully understand — especially in your first months.

---

## Task 5 — Critical Communication Cases

| Scenario | Correct Response |
|---|---|
| L2 unavailable for 30+ minutes on a critical alert | Call L2 → then L3 → then your manager. Know where emergency contacts are. |
| Slack/Teams account compromise — need to verify with affected user | **Never** contact them through the breached platform — use phone or alternative channel |
| Sudden surge of critical alerts | Prioritise per workflow and immediately inform your L2 on shift |
| Realised days later you misclassified an alert | Reach out to L2 immediately — threat actors can be silent for weeks before acting |
| Logs not parsed or searchable — can't complete triage | Investigate what you can, report the issue to L2 or a SOC engineer. Don't skip the alert. |

Should you first try to contact your manager in case of a critical threat (Yea/Nay)?
- Nay

Should you immediately contact your L2 if you think you missed the attack (Yea/Nay)?
- Yea

---

## Key Takeaways

- Alert reports preserve investigation context permanently and give L2 a head start
- Follow the **5 Ws** — Who, What, When, Where, Why — for every report
- Escalate when the threat is real, requires action, or is beyond your current understanding
- **Never use a compromised channel** to contact the affected user — always use an alternative
- When in doubt, escalate and communicate — missed threats can have devastating consequences