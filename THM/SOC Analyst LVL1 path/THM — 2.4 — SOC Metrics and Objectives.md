> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #soc-metrics #kpi #sla #mttd #mtta #mttr #blue-team #l1-analyst

---

## Overview

Covers how SOC team efficiency is measured using key metrics like False Positive Rate and MTTD/MTTA/MTTR, why they matter for L1 analysts, and how to improve them.

---

## Task 2 — Core SOC Metrics

| Metric | Formula | Measures |
|---|---|---|
| **Alerts Count** | AC = Total Alerts Received | Overall load on SOC analysts |
| **False Positive Rate** | FPR = False Positives / Total Alerts | Level of noise in alerts |
| **Alert Escalation Rate** | AER = Escalated Alerts / Total Alerts | Experience and independence of L1 analysts |
| **Threat Detection Rate** | TDR = Detected Threats / Total Threats | Reliability of the team |

### Metric Benchmarks

| Metric | Ideal | Problem Threshold |
|---|---|---|
| Alerts Count | 5–30 per analyst per day | Too low = visibility gaps; too high = analyst fatigue |
| False Positive Rate | As low as possible | 80%+ is a serious problem |
| Alert Escalation Rate | Below 20–50% | Too high = L1 lacks experience or confidence |
| Threat Detection Rate | **100%** | Any missed threat can be devastating |

> A high False Positive rate causes **alert fatigue** — analysts start treating every alert as noise and miss real threats. Fixed through **False Positive Remediation** — tuning tools and detection rules.

Is zero alerts for one month a good sign for your SOC team? (Yea/Nay)
- Nay

What is the False Positive Rate if only 10 out of 50 alerts appear to be real threats?
- 80%

---

## Task 3 — SLA Metrics: MTTD, MTTA, MTTR

Grouped into a **Service Level Agreement (SLA)** — a document between the SOC and company management (or MSSP and its customers) defining response time requirements.

![](Pasted%20image%2020260502005911.png)

| Metric | Common Target | Description |
|---|---|---|
| **Team Availability** | 24/7 | Working schedule — 8/5 or 24/7 |
| **Mean Time to Detect (MTTD)** | 5 minutes | Average time between the attack and detection by tools |
| **Mean Time to Acknowledge (MTTA)** | 10 minutes | Average time for L1 to start triaging a new alert |
| **Mean Time to Respond (MTTR)** | 60 minutes | Average time for the team to actually stop the breach |

Imagine a scenario where the SOC team receives a critical alert on Saturday.  
If the team works 8/5, on which day of the week will they acknowledge the alert?
- Monday

Imagine a scenario where an employee was lured into running data stealer malware.  
  1. The SOC team received the "Connection to Redline Stealer C2" alert after **12** minutes.  
  2. One of the L1 analysts on shift moved the alert to In Progress **10** minutes later.  
  3. After **6** minutes, the alert was escalated to L2, who spent **35** minutes cleaning the malware.  
Provide the MTTD, MTTA, and MTTR via comma as your answer (e.g. 10,20,30).
- 12,10,51

---

## Task 4 — Improving the Metrics

| Issue | Recommendations |
|---|---|
| **FPR over 80%** | Exclude trusted activities (e.g. system updates) from SIEM rules; automate triage for common alerts using SOAR or scripts |
| **MTTD over 30 min** | Ask engineers to increase detection rule frequency; verify logs are collected in real-time without delay |
| **MTTA over 30 min** | Ensure analysts get real-time alert notifications; distribute alerts evenly across analysts on shift |
| **MTTR over 4 hours** | Escalate threats to L2 as quickly as possible; ensure the team has documented response procedures for different attack scenarios |

What is the highest acceptable False Positive Rate for SOC teams?
- 80%

Should all SOC roles work together to keep metrics improving? (Yea/Nay)
- Yea

---

## Task 5 — Metrics Lab
#### 1- Unhappy Customer
![](Pasted%20image%2020260502010224.png)
#### 2- Delayed Alert
![](Pasted%20image%2020260502010315.png)
#### 3- Tired Analysts
![](Pasted%20image%2020260502010416.png)

| Challenge                         | Flag                                      |
| --------------------------------- | ----------------------------------------- |
| First scenario (Unhappy Customer) | _THM{mttr:quick_start_but_slow_response}_ |
| Second scenario (Delayed Alert)   | _THM{mttd:time_between_attack_and_alert}_ |
| Third scenario (Tired Analysts)   | _THM{fpr:the_main_cause_of_l1_burnout}_   |

---

## Key Takeaways

- **Alerts Count** should be 5–30 per analyst per day — too few or too many both indicate problems
- **False Positive Rate** above 80% causes alert fatigue and missed threats — tune detection rules
- **Threat Detection Rate** must always be 100% — every missed threat risks ransomware or data exfiltration
- **MTTD → MTTA → MTTR** is the timeline from attack to resolution — all three are tracked in the SLA
- L1 analysts are the first to notice metric issues — communicate them and propose fixes proactively