**Course**: Network Forensics (IT433) — Luxor Faculty of Computers and Information

> **Instructor**: Dr. Hosny Ahmed Abbas



---



## 📘 Lecture 1: Introduction to Forensics & Digital Forensics



### 1. Core Concept

Forensics is the application of scientific methods to collect, analyze, and present evidence for legal proceedings — **digital forensics** extends this to digital information and devices.



### 2. Key Points

- **Forensics** = use of science and technology to investigate facts in courts of law (from Latin *forēnsis* — "of or before the forum")

- Forensic investigation involves: **identification → acquisition → analysis → report**

- **5WH** framework: Who, Where, What, When, Why — defines investigation objectives

- **Crime reconstruction**: forming a hypothesis about events, then testing whether it's possible

- **7 Forensic Science Principles**: Individuality, Progressive Change, Comparison, Analysis, Locard's Exchange, Probability, Circumstantial Facts

- **Digital forensics** = forensic science applied to digital information

- **Digital archaeology** (human behavior traces) vs **Digital geology** (system-generated traces) — the goal is usually digital archaeology, but understanding geology is a prerequisite

- **DFIR** (Digital Forensics and Incident Response) — focuses on identification, investigation, and remediation of cyberattacks

- Digital forensic process: **Collection → Examination → Analysis → Reporting**

- Types of digital evidence: Logs, Video footage, Archives, Active data, Metadata (EXIF), Residual data, Volatile data, Replicant data



### 3. Must-Know Details

| Term                               | Definition                                                                           |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| **Locard's Principle of Exchange** | Whenever two entities come in contact, they exchange traces                          |
| **Law of Individuality**           | Every object has a unique characteristic not duplicated in any other                 |
| **Law of Progressive Change**      | Everything changes with the passage of time                                          |
| **Law of Circumstantial Facts**    | "Facts do not lie, men can and do"                                                   |
| **Chain of Custody**               | Documentation of acquisition, control, analysis, and disposition of evidence         |
| **Evidence Integrity**             | Preservation of evidence in its original form                                        |
| **Forensically Sound**             | Investigation adheres to established digital forensics principles/standards          |
| **Digital Evidence**               | Any digital data containing reliable info that supports or refutes a hypothesis      |
| **Evidence Dynamics**              | Any influence that adds, changes, or relocates digital evidence                      |
| **Incident Response (IR)**         | A business's plan when experiencing a cyber security attack                          |
| **Cyber Incident**                 | Any event compromising **confidentiality, integrity, or availability** (CIA) of data |



**Types of Crimes:**

- **Advanced cybercrime** — sophisticated attacks against HW/SW

- **Cyber-aided crime** — traditional crimes using the Internet

- **Crimes with digital evidence** — suspect has digital devices



**Key Tools:** FTK Imager (imaging), Autopsy (analysis), AccessData Registry Viewer (registry), MyRecover (file recovery), PRTK (password cracking)



### 4. Common Traps

- ⚠️ **Digital archaeology ≠ Digital geology** — archaeology is about *human* behavior traces; geology is about *system* traces. The exam goal is archaeology, but you must understand geology first.

- ⚠️ **Forensics ≠ only criminal law** — it applies to both criminal AND private/civil law.

- ⚠️ **Volatile data** (e.g., RAM viruses) is never written to disk — it vanishes on shutdown.

- ⚠️ **Residual data** (deleted/overwritten) is *different* from **Replicant data** (cache, cookies, temp files).

- ⚠️ "Digital evidence is **hard to get and easy to destroy**" — remember this quote.



### 5. Quick Recall

Forensics applies science to investigate evidence for courts; digital forensics extends this to digital devices and data. The 7 principles (especially Locard's Exchange) govern the science, while the process follows Collection → Examination → Analysis → Reporting. Key terms to remember: chain of custody, evidence integrity, forensically sound, and the difference between volatile/residual/replicant data.



---



## 📗 Lecture 2: Computer Forensics



### 1. Core Concept

Computer forensics examines digital devices (storage, memory, registry) to extract and preserve evidence, using techniques for maintaining **evidence integrity** and understanding data structures like file systems, encoding, hashing, and the Windows Registry.



### 2. Key Points

- **Evidence integrity** = evidence must NOT be changed by the examiner; required for admissibility

- **Chain of custody** = logical sequence recording custody, control, transfer, analysis, disposition — if broken, evidence is **inadmissible**

- Maintaining chain of custody: **document every step**, **hash forensic images**, use **write-blocking devices**

- **HDD vs SSD**: HDD allows easier data recovery; SSD has garbage collection & wear levelling that make recovery very difficult

- **SSD structure**: Blocks → Pages → Cells. Reading/writing at **page** level; erasing at **block** level

- **HDD**: data not completely erased on deletion; recovery possible if not overwritten. Uses **sectors and clusters**

- **Partition tables**: MBR or GUID; reformatting often only removes the table, data may remain recoverable

- **File systems**: ext4, NFS, FAT32, NTFS — structures data on partitions

- **File structure**: Header (with file signature/magic bytes) → Data → Trailer

- **Encoding**: ASCII, UTF-8, UTF-16 — "A" = `41` (ASCII) vs `feff0041` (UTF-16)

- **Windows Registry**: hierarchical database (tree structure, up to 512 keys deep) with hives: **SAM, SECURITY, SYSTEM, SOFTWARE, NTUSER.dat**



### 3. Must-Know Details



**File Signatures (Magic Bytes):**

| File Type | Hex Signature    |
| --------- | ---------------- |
| **JPEG**  | `FF D8 FF E0`    |
| **PDF**   | `25 50 44 46 2D` |



**Data Representation:**

- **Big-endian**: most significant byte first

- **Little-endian**: least significant byte first



**Encryption vs Hashing vs Salting:**

| Concept        | Direction              | Purpose                                                              |
| -------------- | ---------------------- | -------------------------------------------------------------------- |
| **Encryption** | Two-way (reversible)   | Scramble data, can unscramble later                                  |
| **Hashing**    | One-way (irreversible) | Map data to fixed-length value; used for authentication              |
| **Salting**    | Added to hashing       | Extra value appended to password before hashing; changes hash output |



**Windows Registry Hives:**

| Hive           | Contains                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------ |
| **NTUSER.dat** | User-specific info (browser history, app settings)                                               |
| **SOFTWARE**   | Application data; Windows version at `\Microsoft\WindowsNT\CurrentVersion`                       |
| **SYSTEM**     | USB devices connected, time zone (`\SYSTEM\ControlSet001\Control\TimeZoneInformation`), networks |
| **SAM**        | User accounts, last logon, account creation dates, password hashes                               |
| **SECURITY**   | System audit policy, Syskey (needed with SAM for password cracking)                              |



**Memory & Paging:**

- RAM is volatile — cleared on reboot

- **Paging**: when RAM overflows → data stored in `pagefile.sys` on disk

- RAM can contain: passwords, encrypted emails, decrypted content



**Notable Artifacts & Locations:**

| Artifact         | Location / Description                                                            |
| ---------------- | --------------------------------------------------------------------------------- |
| **Prefetch**     | `c:\Windows\` — shows previously executed programs                                |
| **Shellbags**    | `USRCLASS.DAT\...\Shell\BagMRU` — GUI folder settings                             |
| **.LNK Files**   | `\AppData\Roaming\Microsoft\Windows\Recent` — shortcuts, NOT deleted when file is |
| **Thumbcache**   | `\AppData\Local\Microsoft\Windows\Explorer` — picture thumbnails, NOT deleted     |
| **Event Viewer** | `\System32\winevt\Logs` — program/security/system events                          |
| **USB History**  | `\Windows\INF`                                                                    |



### 4. Common Traps

- ⚠️ **SSD ≠ HDD for forensics**: SSD garbage collection can **auto-delete data within minutes** of idle time — don't assume SSD evidence is recoverable like HDD.

- ⚠️ **Reformatting ≠ data destruction**: Often only the partition table is removed; actual data remains until overwritten.

- ⚠️ **SAM and SECURITY hives** cannot be browsed with `regedit` on a running system — you must extract them from a forensic image.

- ⚠️ **.LNK files and Thumbcache** are **not deleted** when the original file is — they persist as evidence!

- ⚠️ **Encryption is two-way; hashing is one-way** — don't confuse them.

- ⚠️ **Compound files** (Office, ZIP) have internal structure — must be unpacked for full analysis.



### 5. Quick Recall

Computer forensics extracts evidence from storage devices while maintaining evidence integrity and chain of custody. Key concepts: HDD data survives deletion (until overwritten); SSD is harder due to garbage collection. The Windows Registry (SAM, SYSTEM, SOFTWARE, SECURITY, NTUSER.dat) is a goldmine for forensic examiners — revealing users, installed apps, USB history, and timezone info. Always use write-blockers and hash your images.



---



## 📙 Lecture 3: The Digital Forensics Process



### 1. Core Concept

The digital forensics process is a structured, **5-phase methodology** (Identification → Acquisition → Examination → Analysis → Presentation) applied to any device storing digital data, with a critical distinction between **live** and **dead (static)** acquisition.



### 2. Key Points

- The 5 phases are **consecutive but iterative** — you can go back to earlier phases

- **Identification Phase**: detect the incident, apply 5WH, identify evidence sources, isolate/secure/document devices, form an initial hypothesis, follow SOPs

- **Acquisition/Collection Phase**: create forensic copies (never work on originals!), photograph the scene, dump volatile memory first, label evidence (case name, number, examiner, timestamps, location, timezone)

- **Digital fingerprinting** using cryptographic hashes: **MD5, SHA-1, SHA-256**

- **Live Acquisition**: data from a running system (RAM + HDD if encrypted). Can't be repeated exactly — alters data

- **Dead (Static) Acquisition**: data from powered-off system. Doesn't alter data — repeatable

- **RAM contains**: executed programs, passwords, usernames, web pages (even private mode!), decrypted content, network traffic, content never written to disk

- **RAM data is NOT timestamped** — important limitation

- **Examination Phase**: triage (identify most relevant data quickly), data recovery, filtering, handle encryption/steganography/obfuscation

- **Analysis Phase**: connect the dots — use timelining, data mining, statistical methods, linking data objects

- **Presentation Phase**: report findings in layman language, include chain of custody, visualizations, support reproducibility



### 3. Must-Know Details



**Live vs Dead Acquisition:**

| Feature         | Live Acquisition              | Dead (Static) Acquisition |
| --------------- | ----------------------------- | ------------------------- |
| System state    | Running                       | Powered off               |
| Data alteration | YES — alters data             | NO — data unchanged       |
| Repeatable?     | No (not exactly)              | Yes                       |
| Use case        | RAM capture, encrypted drives | Physical disk imaging     |
| Types           | Logical image, Virtual image  | Physical Disk/USB image   |



**Key Tools:**

| Tool                  | Purpose                                  |
| --------------------- | ---------------------------------------- |
| **Volatility**        | Advanced memory forensics framework      |
| **EDD.exe**           | Encrypted Disk Detector                  |
| **FTK Imager**        | Create forensic images                   |
| **Disk2Vhd**          | Convert physical disk to virtual machine |
| **Autopsy**           | Disk/memory image analysis               |
| **Registry Explorer** | Registry analysis                        |



**Forensic Process Practice Workflow:**

1. Image RAM → Capture Memory

2. Check for Disk Encryption → EDD.exe

3. Create Quick Triage Image → FTK Imager (Custom Content Image)

4. Begin Analysis of Triage Image → Analysis Tools

5. Image Entire Hard Disk → FTK Imager (Create Disk Image)



**Presentation Report Must Include:**

- Roles and tasks assigned

- Executive summary

- Forensic acquisition reflecting chain of custody and evidence integrity

- Visualizations, diagrams, images, screenshots

- Information supporting repeatability/reproducibility

- Tools used and findings



### 4. Common Traps

- ⚠️ **Always work on COPIES, never originals** — this is a fundamental rule.

- ⚠️ **Live acquisition is now preferred** (not dead) — because of HDD encryption prevalence. Dead *used to be* the standard.

- ⚠️ **RAM data has NO timestamps** — you cannot determine *when* something was in memory.

- ⚠️ **Live acquisition alters the data** — which means it's NOT exactly repeatable.

- ⚠️ **Examination ≠ Analysis**: Examination is extracting/preparing data; Analysis is interpreting and connecting dots.

- ⚠️ **Steganography** (hiding data within other data like images) is specifically mentioned as a challenge in the examination phase.



### 5. Quick Recall

The digital forensics process has 5 iterative phases: Identification (what happened? 5WH), Acquisition (copy evidence — never touch originals; live preferred now due to encryption), Examination (triage and extract data), Analysis (connect dots, build timelines), and Presentation (report in layman terms). RAM captures are critical because they contain passwords, decrypted content, and data never written to disk — but RAM data has NO timestamps.



---



## 📕 Lecture 4: Network Forensics



### 1. Core Concept

Network forensics is the monitoring and analysis of **volatile, dynamic** network traffic for legal evidence and intrusion detection, requiring proactive investigation using the **OSCAR** methodology and multiple evidence sources across the network infrastructure.



### 2. Key Points

- Network forensics deals with **volatile and dynamic** information — traffic is transmitted and then lost

- Network forensics is often **proactive** (set up before breaches) because data disappears quickly

- Network evidence may be the **only evidence** if an attacker erases host log files

- **Marcus Ranum** defined network forensics as "the capture, recording, and analysis of network events to discover the source of security attacks"

- Two collection approaches: **"Catch-it-as-you-can"** (capture everything) vs **"Stop, look and listen"** (capture only suspicious traffic)

- **OSCAR Methodology**: **O**btain info → **S**trategize → **C**ollect evidence → **A**nalyze → **R**eport

- Evidence acquisition types: **Passive** (no data emitted at Layer 2+) vs **Active/Interactive** (interacting with live network devices)

- Physical interception methods: Inline Network Taps, Vampire Taps, Induction Coils, Fiber Optic Taps

- Traffic acquisition software relies on **libpcap** (UNIX) and **WinPcap** (Windows) — both BSD-licensed

- Key tools: tcpdump, Wireshark, Snort, nmap, ngrep, NetworkMiner



### 3. Must-Know Details



**OSCAR Methodology — Detailed:**

| Phase              | Key Activities                                                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **O — Obtain**     | Incident description, date/time of discovery, persons/systems involved, legal issues, environment (network topology, business model), goals                        |
| **S — Strategize** | Understand goals/timeframe, list resources, identify evidence sources, estimate value/cost, prioritize acquisition, plan initial acquisition                       |
| **C — Collect**    | Three sub-steps: **Document** (log all actions), **Capture** (packets, logs, images), **Store/Transport** (maintain chain of custody)                              |
| **A — Analyze**    | Correlation, Timeline building, Events of Interest, Corroboration (avoid false positives!), Recovery of additional evidence, Interpretation (always a hypothesis!) |
| **R — Report**     | Understandable by non-technical people, Defensible in detail, Factual, use executive summaries                                                                     |



**6 Tips for Evidence Collection:**

1. Acquire as soon as possible, and **lawfully**

2. Make **cryptographically verifiable copies**

3. Sequester the originals under restricted custody

4. **Analyze only the copies**

5. Use reputable and reliable tools

6. **Document everything you do!**



**Network Forensics Challenges:**

- Acquisition (hard to locate specific evidence)

- Content (varying granularity)

- Storage (no persistent storage on network devices)

- Privacy (legal issues)

- Seizure (very disruptive)

- Admissibility (conflicting legal precedents)



**Sources of Network-Based Evidence:**

| Source                 | Evidence Type                                    |
| ---------------------- | ------------------------------------------------ |
| On the Wire            | Physical cable tapping                           |
| In the Air             | Wireless captures (need encryption key)          |
| Switches               | CAM table, Mirror/SPAN ports                     |
| Routers                | Routing tables, logs, packet filters             |
| DHCP Servers           | DHCP logs                                        |
| DNS Servers            | DNS logs (timeline of suspect activities)        |
| Authentication Servers | Login attempts, brute force attacks              |
| NIDS/NIPS              | Alerts, logs (can be tuned for more granularity) |
| Firewalls              | Allowed/denied traffic, IPs, ports, protocols    |
| Web Proxies            | Cached pages, web surfing logs                   |
| Application Servers    | DB, web, email server logs                       |
| Central Log Servers    | Aggregated event logs                            |



**Strategy for Evidence Acquisition (5 steps):**

1. Don't reboot or power down the device

2. Connect via **console** rather than network

3. Record system time

4. Collect by **level of volatility** (most volatile first)

5. Record your investigative activities



**DFIR Triggers:**

- **Reactive**: An event or incident

- **Proactive**: Vulnerability assessment exercise



### 4. Common Traps

- ⚠️ **Network evidence is VOLATILE** — unlike disk forensics where evidence persists, network data vanishes in milliseconds.

- ⚠️ **"Catch-it-as-you-can" vs "Stop, look and listen"** — know the trade-offs: full capture = time/storage heavy; selective capture = needs processing power, may miss things.

- ⚠️ **Passive ≠ Active acquisition**: Passive gathers evidence WITHOUT emitting data (Layer 2+); Active INTERACTS with devices.

- ⚠️ **Interpretation is always a HYPOTHESIS** — never present your analysis as absolute fact.

- ⚠️ **Corroboration**: Always verify events through **multiple sources** to avoid false positives.

- ⚠️ **Forensics is ITERATIVE** — after initial analysis you may need to go back and acquire more evidence.

- ⚠️ Network devices often **cannot be seized** without disrupting business operations.



### 5. Quick Recall

Network forensics deals with volatile, dynamic traffic that vanishes quickly — making it often proactive. Use the OSCAR methodology: Obtain info, Strategize, Collect evidence (document + capture + store), Analyze (correlate, timeline, corroborate), Report (in layman terms). Evidence sources span the entire infrastructure — from wire taps and switches (SPAN ports) to DNS logs, firewalls, and central log servers. Always collect by volatility level (most volatile first) and never reboot the device.



---



## 📓 Lecture 5: Packet Capture and Analysis



### 1. Core Concept

Packet capture is the practice of intercepting and recording network traffic using hardware (TAPs, SPAN ports) and software tools (Wireshark, tcpdump), with analysis performed through packet decoding, filtering, stream following, and file extraction.



### 2. Key Points

- Packet capture shows exactly what happens on the wire — **true and accurate** with nothing in the way

- **Promiscuous mode**: when a NIC captures ALL messages, not just those addressed to it

- Capture locations: **on an endpoint** (install software) or **on the network** (via hubs, switches, TAPs)

- **Hubs**: broadcast all traffic to every node — NIC must be in promiscuous mode

- **Switches (SPAN/Mirror ports)**: enterprise switches copy traffic to a designated SPAN port; copies both RX and TX; **active mode** (switch does the copying); drawbacks: network overload, CPU resources, low priority

- **TAPs**: passive mode, court-approved, no MAC address, no IP address, can't be hacked, **fail-open** (network continues if TAP fails), separate ports for each traffic direction

- **TAPs > SPANs** for forensics — TAPs are passive, court-approved, and more reliable

- **Command-line tools**: tcpdump (Unix, decades old), tshark

- **GUI tools**: Wireshark (originally Ethereal, by Gerald Combs in 1998), NetworkMiner

- Wireshark features: **dissectors** (protocol-specific modules), packet decoding, filtering, statistics, following streams, gathering files

- **ARP Spoofing** and **Port Spanning** are techniques mentioned for capturing traffic

- tcpdump commands: `sudo tcpdump` (basic), `tcpdump -v` (verbose), `tcpdump -s 0 -w capture.pcap` (full capture to file)



### 3. Must-Know Details



**Capture Methods Comparison:**

| Method               | Mode                    | Pros                                                  | Cons                                                     |
| -------------------- | ----------------------- | ----------------------------------------------------- | -------------------------------------------------------- |
| **Hub**              | Passive (broadcast)     | Simple, captures all traffic                          | Legacy technology, rare today                            |
| **SPAN/Mirror Port** | Active (switch copies)  | No extra hardware                                     | CPU intensive, low priority, may miss packets under load |
| **TAP**              | Passive (physical copy) | Court-approved, no MAC/IP, can't be hacked, fail-open | Requires physical installation                           |



**TAP Key Properties (memorize):**

- ✅ Passive mode

- ✅ Court-approved

- ✅ No MAC address

- ✅ No IP address

- ✅ Can't be hacked

- ✅ Fail-open (network stays up if TAP fails)

- ✅ Separate ports for each direction



**Key tcpdump Commands:**

| Command                             | Action                                   |
| ----------------------------------- | ---------------------------------------- |
| `sudo tcpdump`                      | Print summary headers of captured frames |
| `sudo tcpdump -v`                   | Verbose output                           |
| `sudo tcpdump -s 0 -w capture.pcap` | Full packet capture, write to .pcap file |



**Wireshark History:**

- Created in **1998** by **Gerald Combs**

- Originally called **Ethereal**, later renamed **Wireshark**

- Uses **dissectors** (protocol-decoding modules)

- May require **administrative privileges**



**Software Libraries:**

- **libpcap** — UNIX C library for packet capture

- **WinPcap** — Windows equivalent

- Both released under **BSD license**



**Wireshark Analysis Features:**

1. Packet Decoding

2. Filtering

3. Statistics

4. Following Streams

5. Gathering Files



### 4. Common Traps

- ⚠️ **SPAN ports are ACTIVE mode** (switch does the copying) — TAPs are PASSIVE. Don't mix them up.

- ⚠️ **SPAN ports can miss packets** under network overload because copying is low-priority for the switch.

- ⚠️ **TAPs have no MAC/IP** — they can't be hacked or detected on the network. This is why they're court-approved.

- ⚠️ **Promiscuous mode** is needed for hubs (broadcast networks) — Wireshark enables this automatically.

- ⚠️ **tcpdump requires sudo/admin** — so does Wireshark in some cases.

- ⚠️ **Wireshark ≠ Ethereal** — same software, different name. Don't call it Ethereal on the exam.

- ⚠️ **Fail-open** means the network continues working even if the TAP device fails — this is a feature, not a flaw.



### 5. Quick Recall

Packet capture records exactly what's on the wire. Capture using TAPs (passive, court-approved, no MAC/IP, fail-open) or SPAN ports (active, switch copies traffic, may miss packets under load). Key tools: tcpdump (CLI, `sudo tcpdump -s 0 -w capture.pcap`) and Wireshark (GUI, originally Ethereal by Gerald Combs in 1998, uses dissectors). Always put NIC in promiscuous mode to see all traffic.



---

---



# 🏆 MASTER CHEAT SHEET — Network Forensics (IT433)



> **This merges the most critical, testable points across all 5 lectures.**



## ⚖️ Foundational Principles

| Principle              | Meaning                                                                            |
| ---------------------- | ---------------------------------------------------------------------------------- |
| **Locard's Exchange**  | Contact between two entities = trace exchange                                      |
| **Chain of Custody**   | Document every step of evidence handling — if broken, evidence is **inadmissible** |
| **Evidence Integrity** | Evidence must NOT be altered by the examiner                                       |
| **Forensically Sound** | Investigation follows established principles/standards                             |



## 🔄 The Digital Forensics Process (5 Phases)

```
Identification → Acquisition → Examination → Analysis → Presentation
     (5WH)       (copy, hash)   (triage)     (timeline)   (report)
```

- Phases are **consecutive but iterative**

- Always work on **COPIES**, never originals

- Hash images with **MD5 / SHA-1 / SHA-256**



## 🔴 OSCAR Methodology (Network Forensics)

```
O — Obtain info (incident + environment)
S — Strategize (plan, prioritize, estimate)
C — Collect (Document + Capture + Store/Transport)
A — Analyze (Correlate, Timeline, Corroborate, Interpret)
R — Report (layman language, factual, defensible)
```



## 💾 Storage Forensics

|                      | HDD                               | SSD                                     |
| -------------------- | --------------------------------- | --------------------------------------- |
| **Data on deletion** | Still there (until overwritten)   | Garbage collection may erase in minutes |
| **Recovery**         | Fully possible if not overwritten | Very difficult (manufacturer-dependent) |
| **Structure**        | Sectors & Clusters                | Blocks → Pages → Cells                  |
| **Erasure level**    | Sector                            | Block                                   |
| **Read/Write level** | Sector                            | Page                                    |



## 🗂️ Windows Registry Hives

| Hive           | What it stores                         |
| -------------- | -------------------------------------- |
| **SAM**        | Users, logon times, password hashes    |
| **SECURITY**   | Audit policy, Syskey                   |
| **SYSTEM**     | USB devices, timezone, networks        |
| **SOFTWARE**   | Apps, Windows version/install date     |
| **NTUSER.dat** | Per-user browser history, app settings |



## 🔐 Encryption / Hashing / Salting

- **Encryption**: Two-way (reversible)

- **Hashing**: One-way (irreversible), fixed-length output

- **Salting**: Extra value added before hashing — changes the hash



## 📡 Live vs Dead Acquisition

|                    | Live             | Dead (Static)        |
| ------------------ | ---------------- | -------------------- |
| **System**         | Running          | Powered off          |
| **Alters data?**   | YES              | NO                   |
| **Repeatable?**    | No               | Yes                  |
| **Now preferred?** | YES (encryption) | Was the old standard |



## 🧠 RAM — What It Contains

Passwords, usernames, executed programs, web pages (even private mode), decrypted content, network traffic, content never on disk — **BUT RAM data has NO timestamps**



## 🌐 Network Evidence Sources

Wire → Air → Switches (CAM/SPAN) → Routers → DHCP → DNS → Auth Servers → NIDS/NIPS → Firewalls → Web Proxies → App Servers → Central Log Servers



## 📦 Packet Capture

| Method   | Mode    | Court-Approved?    | Can Be Hacked?   |
| -------- | ------- | ------------------ | ---------------- |
| **TAP**  | Passive | ✅ Yes              | ❌ No (no MAC/IP) |
| **SPAN** | Active  | ❌ Not specifically | Possible         |



## 🛠️ Must-Know Tools

| Tool                           | Purpose                                                             |
| ------------------------------ | ------------------------------------------------------------------- |
| **FTK Imager**                 | Create forensic images                                              |
| **Autopsy**                    | Disk/memory analysis                                                |
| **Volatility**                 | Memory forensics framework                                          |
| **EDD.exe**                    | Encrypted Disk Detector                                             |
| **Wireshark**                  | GUI packet capture/analysis (1998, Gerald Combs, formerly Ethereal) |
| **tcpdump**                    | CLI packet capture (Unix)                                           |
| **NetworkMiner**               | GUI network analysis                                                |
| **AccessData Registry Viewer** | Registry hive analysis                                              |
| **libpcap / WinPcap**          | Packet capture libraries (BSD license)                              |



## 📝 File Signatures

| Type | Hex              |
| ---- | ---------------- |
| JPEG | `FF D8 FF E0`    |
| PDF  | `25 50 44 46 2D` |



## 🧩 Evidence Collection Rules

1. Acquire ASAP, **lawfully**

2. Make **cryptographically verifiable** copies

3. Sequester originals

4. Analyze **only copies**

5. Use reputable tools

6. **Document everything!**



## ⚡ Evidence Acquisition Strategy (Network)

1. **Don't reboot** the device

2. Connect via **console** (not network)

3. **Record system time**

4. Collect by **volatility level** (most volatile first)

5. **Record** all investigative activities



## ❗ Top Exam Traps to Avoid

1. **SSD ≠ HDD** — SSD garbage collection destroys evidence automatically

2. **Reformatting ≠ data destruction** — often only partition table is removed

3. **Live acquisition is now preferred** over dead (because of encryption)

4. **RAM has NO timestamps**

5. **Examination ≠ Analysis** — extraction vs interpretation

6. **.LNK files & Thumbcache persist** even after original file deletion

7. **TAP = passive, SPAN = active** — don't confuse them

8. **Interpretation is always a hypothesis** — never state analysis as absolute fact

9. **Corroborate through multiple sources** to avoid false positives

10. **Encryption = two-way; Hashing = one-way** — never confuse them



---



> 💬 **What's next?** Would you like me to create:
> - 🃏 **Flashcards** for quick memorization?
> - ❓ **Practice exam questions** (MCQ + short answer)?
> - 🔍 **A deeper dive** into any specific topic?
>
> Just let me know!
