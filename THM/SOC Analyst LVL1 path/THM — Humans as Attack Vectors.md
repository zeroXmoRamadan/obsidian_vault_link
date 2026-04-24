# THM — Humans as Attack Vectors

> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #social-engineering #phishing #blue-team #soc #human-factor

---

## Overview

Explores why humans are the weakest link in cyber security, how attackers exploit them through social engineering, and how SOC analysts detect and mitigate these attacks.

**Prerequisites:** [[SOC Role in Blue Team]]  
**Next Rooms:** [[Systems as Attack Vectors]]

---

## Task 2 — Why Humans Are Targeted

Attackers often find it easier to manipulate a human than to breach technical defences — like asking the gatekeeper to open the door rather than breaking it down.

### What Attackers Aim For

|Attack|Attacker's Next Step|
|---|---|
|Breach HR manager's Google account|Steal and sell the entire employee database|
|Trick wealthy person into running malware|Hijack their web banking session|
|Breach IT administrator's account|Access the core of the corporate network|
|Trick government worker into sharing secrets|Use intel to simplify future attacks|

---

## Task 3 — Social Engineering Attack Types

All attacks targeting humans rely on **social engineering** — manipulating victims psychologically rather than exploiting technical flaws.

For an attack to succeed it must be:

- **Trustworthy** — the attacker appears legitimate
- **Emotional** — triggers urgency, fear, or curiosity

### Common Attack Methods

|Attack Type|Description|Example|
|---|---|---|
|**Phishing**|Fraudulent emails/messages with fake links or login pages|"Your account is compromised — click here" leading to a credential-harvesting page|
|**Malware Downloads**|Victims tricked into downloading malicious software|Fake app downloads, fake CAPTCHAs, malicious QR codes, SEO poisoning|
|**Deepfakes**|AI-generated video/audio impersonating trusted individuals|Finance worker tricked into wiring **$25 million** after a fake video call from their "boss"|
|**Impersonation**|Pretending to be IT, management, or a trusted party without deepfakes|Phone calls impersonating IT support asking to take over accounts for "system repair"|
|**Other**|USB drops, physical access attacks, insider threats, fake job offers|Any attack that exploits human trust or curiosity|

> **Scale:** An estimated **3.4 billion** malicious phishing emails are sent daily.

---

## Task 4 — Defending Against Human-Targeted Attacks

Defence requires both **Mitigation** (prevent/reduce attacks) and **Detection** (catch what slips through).

### Key Mitigation Measures

|Measure|Description|
|---|---|
|**Anti-phishing solution**|Automatically blocks malicious emails before users ever see them|
|**Antivirus / EDR**|Prevents malware execution on corporate hosts|
|**"Trust but verify" principle**|Train employees to detect deepfakes and verify suspicious requests from "CEO" or "IT"|
|**Security awareness training**|Teach staff to spot attacks; reinforce with simulated phishing exercises|

> Mitigation reduces workload for analysts and hardens the human layer before incidents occur.

---

## Task 5 — SOC Analyst Role in Human Attack Defence

SOC analysts don't just monitor alerts — they can be deeply embedded in the organisation's defence culture:

- Maintain relationships with IT, HR, and other departments
- Propose and implement security improvements
- Run company-wide security awareness trainings
- Operate employee hotlines for reporting suspected attacks

### Lab — TryHackMe Security Dashboard

|Challenge|Flag|
|---|---|
|Employees at Risk|_(found in lab)_|
|Security Policy|_(found in lab)_|

---

## Key Takeaways

- Humans are the **weakest link** in cyber security — targeted because of the access they provide
- Social engineering exploits **psychology**, not technology — trust and emotion are the weapons
- Phishing is the most common vector — **3.4 billion** malicious emails sent daily
- Deepfakes and impersonation are growing threats requiring a "trust but verify" mindset
- Mitigation (training, tools, policy) reduces risk; detection skills catch what gets through
- SOC analysts play an active role beyond alert monitoring — they help shape security culture

---

## Threat Intel Resources

|Site|URL|
|---|---|
|Krebs on Security|https://krebsonsecurity.com|
|The Hacker News|https://thehackernews.com|
|BleepingComputer|https://www.bleepingcomputer.com|
