> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #soc #blue-team #analyst #career

---

## Overview

An introductory room that simulates the first day on the job as a **Junior Security Analyst (Level 1)**. It covers daily duties, team structure, and ends with a hands-on lab where you investigate a real alert.

---

## Task 1 — The Security Analyst Journey

### Role Summary

- Also known as a **Level 1 Analyst**
- Part of a **24/7 shift-based team**
- First line of defense against cyber threats

### Daily Duties

- Monitor and investigate security alerts
- Participate in brainstorms and workshops
- Cooperate with other teams
- Continuously learn about new attacks and defenses

Which team do you work with as a Junior Security Analyst?
- SOC

---

## Task 2 — Your SOC Team

|Name|Role|Responsibilities|
|---|---|---|
|**Will Griffin**|Senior Analyst|Helps junior analysts, handles complex cases|
|**Corey Stevens**|SOC Engineer|Maintains tools, configures alerts (no shift work)|
|**Emily Conway**|SOC Manager|Reports to leadership, keeps the team on track|
|**Daniel Herrera**|Incident Responder|Called in on-demand for major incidents|

### Career Progression

Over time, a Junior Analyst may:

- Detect and prevent data stealer infections
- Analyze and stop phishing/finance-targeting campaigns
- Participate in major incidents (e.g., ransomware response)
- Build detection rules and automations
- Develop broader understanding of business operations

---

## Task 3 — Being a Security Analyst (Lab)

### Key Points

- Shifts are busy — analysts work through a queue of **tickets** (alerts + tasks)
- Requires constant learning and adaptability
- Rewarding when real threats are stopped

### Lab Questions

![](Pasted%20image%2020260424171759.png)

| Question                                       | Answer                                                                     |
| ---------------------------------------------- | -------------------------------------------------------------------------- |
| Malicious IP address in the alerts             | ![](Pasted%20image%2020260424171817.png)<br><br>_221.181.185.159_          |
| Who was the alert escalated to?                | ![](Pasted%20image%2020260424171839.png)<br><br>_Will Griffin_             |
| Message after blocking the IP on the firewall? | ![](Pasted%20image%2020260424171900.png)<br><br>_THM{until-we-meet-again}_ |

> **Note:** Complete the interactive lab by clicking **View Site** in Task 3 to get the answers above.

---

## Key Takeaways

- The SOC operates 24/7 with tiered roles (L1 analyst → senior analyst → manager/IR)
- L1 analysts focus on **triage and initial investigation**, then escalate
- Practical skills matter — this path involves hands-on alert analysis from day one
- Threat awareness (reading cyber news, understanding TTPs) is part of the job