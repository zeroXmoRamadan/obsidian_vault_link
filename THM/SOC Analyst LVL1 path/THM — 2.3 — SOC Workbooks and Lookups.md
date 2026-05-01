> **Platform:** TryHackMe  
> **Path:** SOC Level 1  
> **Difficulty:** Easy  
> **Tags:** #tryhackme #workbooks #lookups #asset-inventory #network-diagrams #soc #blue-team #l1-analyst

---

## Overview

Covers how L1 analysts gather context during alert triage using identity and asset inventories, network diagrams, and investigation workbooks to ensure consistent, high-quality analysis.

---

## Task 2 — Identity & Asset Inventory

### Identity Inventory

A catalogue of corporate employees, service accounts, and their details — roles, privileges, contacts, and access levels.

| Full Name | Username | Role | Location | Access |
|---|---|---|---|---|
| Gregory Baker | G.Baker | Chief Financial Officer | Europe, UK | SIEM, HQ, FINANCE |
| Raymond Lund | R.Lund | US Financial Adviser | US, Texas | SIEM, FINANCE |
| Kate Danner | K.Danner | Chief Technology Officer | Europe, UK | SIEM, DA, HQ |
| svc-veeam-06 | svc-veeam-06 | Backup Service Account | N/A | VEEAM, HQ |

**Sources of Identity Data:**

| Solution | Examples | Description |
|---|---|---|
| **Active Directory** | On-prem AD, Entra ID | Core identity database, commonly used by SIEM |
| **SSO Providers** | Okta, Google Workspace | Cloud alternative for AD |
| **HR Systems** | BambooHR, SAP, HiBob | Full employee data, limited to staff only |
| **Custom Solution** | CSV / Excel Sheets | Maintained by IT or security teams |

---

### Asset Inventory

A list of all computing resources (servers, workstations) in the organisation's IT environment.

| Hostname | Location | IP Address | OS | Purpose |
|---|---|---|---|---|
| HQ-FINFS-02 | UK Datacenter | 172.16.15.89 | Windows Server 2022 | File server for financial records |
| HQ-ADDC-01 | UK Datacenter | 172.16.15.10 | Windows Server 2019 | Primary domain controller |
| PC-891D | London Office | 192.168.5.13 | Windows 11 Pro | Stationary PC for accountants |
| L007694 | Remote | N/A | MacOS 13 | Corporate laptop |

**Sources of Asset Data:**

| Solution | Examples | Description |
|---|---|---|
| **Active Directory** | On-prem AD, Entra ID | Also functions as an asset inventory database |
| **SIEM / EDR** | Elastic, CrowdStrike | Agents collect host information during monitoring |
| **MDM Solution** | MS Intune, Jamf | Dedicated solution to list and manage devices |
| **Custom Solution** | CSV / Excel Sheets | Common in smaller teams |

Looking at the identity inventory, what is the role of R.Lund at the company?
- US Financial Adviser

Checking the asset inventory, what data does the HQ-FINFS-02 server store?
- Financial records

Finally, does the file sharing from the scenario look legitimate and expected? (Yea/Nay)
- Yea

---

## Task 3 — Network Diagrams

A **network diagram** is a visual schema of an organisation's locations, subnets, and their connections. Essential when investigating alerts involving IP addresses and lateral movement.

### Example Attack Reconstruction

| Time | Event |
|---|---|
| 08:00 | External IP `103.61.240.174` repeatedly connects to corporate VPN via port 443/10443 |
| 08:23 | NAT logs show the IP was translated to internal `10.10.0.53` |
| 08:25 | `10.10.0.53` scans the `172.16.15.0/24` subnet — no open ports found |
| 08:32 | Same IP now scanning `172.16.23.0/24` — attack ongoing |

![](Pasted%20image%2020260501235332.png)

Using the network diagram, the attack path becomes clear: brute force on VPN → assigned internal IP → attempted lateral movement across subnets.

According to the network diagram, which service is exposed on the TCP/10443 port?
- VPN

Now, which subnet would the server behind 172.16.15.99 IP belong to?
- Database subnet

Finally, does the scenario look like a True Positive (TP) or False Positive (FP)?
- TP

---

## Task 4 — Investigation Workbooks

A **workbook** (also called playbook, runbook, or workflow) is a structured document defining the steps to investigate and remediate a specific threat consistently.

> Senior analysts build workbooks to support L1 analysts — following them ensures no vital steps are skipped.

### Workbook Structure — Unusual Login Location Example

![](Pasted%20image%2020260501235419.png)

| Phase | Steps |
|---|---|
| **1. Enrichment** | Use Threat Intelligence and identity inventory to gather context about the affected user |
| **2. Investigation** | Using gathered data and logs, determine if the login was expected |
| **3. Escalation** | Escalate to L2 or contact the user directly if the login appears suspicious |

Which SOC role would use workbooks the most (e.g. SOC Manager)?
- SOC L1 Analyst

What is the process of gathering user, host, or IP context using TI and lookups?
- Enrichment

Looking at the workbook example, what platform is used as an identity inventory source?
- BambooHR

---

## Task 5 — Building Workbooks

### Lab — Workbook Builder

| Challenge | Flag |
|---|---|
| First workbook | _THM{...}_ |
| Second workbook | _THM{...}_ |
| Third workbook | _THM{...}_ |

---

## Key Takeaways

- **Identity inventory** answers *who* — roles, access, and contact details for users and service accounts
- **Asset inventory** answers *where* — hostname, IP, OS, and purpose of every device
- **Network diagrams** answer *how* — subnet layout helps reconstruct attack paths from raw IPs
- **Workbooks** ensure consistent, high-quality triage by guiding L1 analysts step by step
- Always use available lookups before making a verdict — context is everything in alert triage