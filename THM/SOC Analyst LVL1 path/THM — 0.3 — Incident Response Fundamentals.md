> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #incident-response #blue-team #soc #frameworks #playbooks

---

## Overview

Covers the full lifecycle of incident response — from what counts as an incident, through severity levels, incident types, response frameworks (SANS & NIST), detection tools, and playbooks. Ends with a hands-on phishing email investigation lab.

---

## Task 2 — Events, Alerts & Incidents

### The Pipeline

```
Processes → Events → Logs → Security Solution → Alert → Analysis → Incident
```

- **Event** — anything logged by a running process (interactive or background)
- **Alert** — triggered when a security solution finds events matching a harmful pattern
- **False Positive** — alert looks dangerous but is harmless on investigation
    - _Example: High data transfer flagged, but it was a scheduled cloud backup_
- **True Positive** — alert is confirmed as genuinely harmful
    - _Example: Phishing email confirmed to contain a malicious attachment_
- **Incident** — a confirmed true positive that requires a response

### Incident Severity Levels

|Severity|Priority|
|---|---|
|**Critical**|Highest — respond immediately|
|**High**|Second priority|
|**Medium**|Third priority|
|**Low**|Lowest priority|

What is triggered after an event or group of events point at a harmful activity?
- Alert

If a security solution correctly identifies a harmful activity from a set of events, what type of alert is it?
- true positive

If a fire alarm is triggered by smoke after cooking, is it a true positive or a false positive?
- false positive

---

## Task 3 — Types of Incidents

|Type|Description|Key Note|
|---|---|---|
|**Malware Infection**|Malicious program damages a system, network, or app|Most common incident type; spread via files (docs, executables, etc.)|
|**Security Breach**|Unauthorized access to confidential data|Critical for businesses where data access must be strictly controlled|
|**Data Leak**|Confidential info exposed to unauthorized parties|Can be intentional _or_ accidental (misconfiguration, human error)|
|**Insider Attack**|Attack originating from within the organization|More dangerous — insiders have greater access than outsiders|
|**DoS / DDoS**|Flooding a system/network with fake requests until it's unavailable|Targets _availability_ — one of the three pillars of cyber security|

> **Note:** Severity of impact depends on the organization. A data leak may be minor for one company but catastrophic for another.

A user's system got compromised after downloading a file attachment from an email. What type of incident is this?
- malware infection

What type of incident aims to disrupt the availability of an application?
- Denial of service 

---

## Task 4 — Incident Response Frameworks

### SANS Framework — "PICERL"

|Phase|Description|Example|
|---|---|---|
|**P — Preparation**|Build IR teams, plans, and deploy security solutions|Employee phishing awareness training|
|**I — Identification**|Detect abnormal behaviour indicating an incident|Unusual outbound data transfer traced to a phishing download|
|**C — Containment**|Minimize impact — isolate affected systems/accounts|Isolate compromised host from the network|
|**E — Eradication**|Remove the threat completely from the environment|Deep malware scan and removal|
|**R — Recovery**|Restore systems from backup or rebuild; test before returning to use|Reimage host, restore exfiltrated data from backup|
|**L — Lessons Learned**|Document gaps; improve detection and response for future incidents|Post-incident review meeting, root cause analysis|

![](Images/6645aa8c024f7893371eb7ac-1718265.png)

### NIST Framework — 4 Phases

|NIST Phase|SANS Equivalent|
|---|---|
|Preparation|Preparation|
|Detection & Analysis|Identification|
|Containment, Eradication & Recovery|Containment + Eradication + Recovery|
|Post-Incident Activity|Lessons Learned|

![](Images/6645aa8c024f7893371eb7ac-1718268.png)

both:
![](Images/6645aa8c024f7893371eb7ac-1723217.png)

### Incident Response Plan

A formally approved document covering procedures before, during, and after an incident. Key components:

- Roles & Responsibilities
- IR Methodology
- Communication plan (including law enforcement)
- Escalation path

The Security team disables a machine's internet connection after an incident. Which phase of the SANS IR lifecycle is followed here?
- containment

Which phase of NIST corresponds with the lessons learned phase of the SANS IR lifecycle?
- Post Incident Activity

---

## Task 5 — Tools & Playbooks

### Detection & Response Tools

| Tool               | Role                                                                               |
| ------------------ | ---------------------------------------------------------------------------------- |
| **SIEM**           | Collects and correlates logs from all sources to identify incidents                |
| **Antivirus (AV)** | Detects and removes known malicious programs via regular scans                     |
| **EDR**            | Advanced endpoint protection; can also contain and eradicate threats automatically |

### Playbooks vs Runbooks

||Playbook|Runbook|
|---|---|---|
|**What it is**|High-level guidelines for responding to a specific incident type|Detailed step-by-step execution of specific tasks within an incident|
|**Scope**|Strategic — what to do|Tactical — exactly how to do it|

### Example Playbook — Phishing Email Incident

1. Notify all stakeholders of the phishing incident
2. Analyze email headers and body to confirm it is malicious
3. Identify and analyze any attachments
4. Determine if any user opened the attachment
5. Isolate infected systems from the network
6. Block the sender

Step-by-step comprehensive guidelines for incident response are known as?
- Playbooks

---

## Task 6 — Practical Lab (Phishing IR Exercise)

**Scenario:** A phishing email with a malicious attachment hits multiple hosts. Investigate scope, contain, and respond.

| Question                                    | Answer                                                                            |
| ------------------------------------------- | --------------------------------------------------------------------------------- |
| Name of the malicious email sender?         | ![](Images/Pasted%20image%2020260424174447.png)<br><br>_Jeff Johnson_                    |
| Threat vector?                              | _Email Attachment_                                                                |
| How many devices downloaded the attachment? | ![](Images/Pasted%20image%2020260424174540.png)<br><br>_3_                               |
| How many devices executed the file?         | ![](Images/Pasted%20image%2020260424174556.png)<br><br>_1_                               |
| Flag at the end of the exercise?            | ![](Images/Pasted%20image%2020260424174622.png)<br><br>_THM{My_First_Incident_Response}_ |

---

## Key Takeaways

- Events become incidents only after analysis confirms a **true positive**
- Severity levels (critical → low) dictate response priority
- Five main incident types: malware, breach, data leak, insider attack, DoS
- **SANS (PICERL)** and **NIST** frameworks both guide structured IR — NIST compresses it into 4 phases
- **Playbooks** provide the _what_; **Runbooks** provide the _how_
- Tools like SIEM, AV, and EDR automate detection and can assist in containment/eradication
