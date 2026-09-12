# TryHackMe: Alert Reporting - Complete Room Writeup

## 📌 Room Overview & Objectives
As a Level 1 (L1) SOC Analyst, triaging alerts is only half the battle. Documentation is critical to ensure that Level 2 (L2) analysts, Incident Responders, and management can seamlessly understand, validate, and remediate threats. 

This room covers the core fundamentals of:
1. **The 5 Ws Framework** for building structured analyst reports.
2. **Alert Life Cycle Management** within a SIEM/Ticketing system (Assignment ➡️ In Progress ➡️ Closure/Escalation).
3. **Escalation Workflows** to senior tiers.
4. **Out-of-Band SOC Communication Channels** during a major incident.

---

## 🛠 Task 2: Introduction to Alert Reporting

### 📖 Key Concepts
* **Alert Reporting:** The process of documenting a security alert's technical findings, timeline, and contextual data. It provides a standardized data format for the entire security team.
* **The Five Ws Matrix:**
  * **Who:** Identifies internal targets (users, workstations) and external actors (attacker IPs, malicious senders).
  * **What:** The specific observed actions, alerts triggered, payloads delivered, or system modifications.
  * **When:** Exact logs and timestamps (in UTC or local SIEM time) mapping out the sequence of events.
  * **Where:** The perimeter boundary, local network segment, endpoint hostname, or specific application directory affected.
  * **Why:** The analytical verdict or evidence proving why the activity is malicious, benign, or suspicious.

### 📝 Task Answers & Flags
* What process ensures details are preserved for future use? 
  `Alert reporting`
* Which user's email was involved in the data leak incident?
  `m.boslan@tryhackme.thm`

---

## 🎣 Task 3: Reporting Guide (Case Study: Phishing Alert)

### 📖 Scenario Analysis
An automated alert triggers for an inbound malicious email targeting a high-profile user workspace.

#### Technical Artifacts Extracted:
* **Target Employee:** Eddie Huffman (`e.huffman@tryhackme.thm`)
* **Display Sender Address:** `support@microsoft.com`
* **Email Theme/Context:** Urgent warning regarding an upcoming Microsoft Teams pricing hike.
* **Payload:** A compressed archive attachment named `REPORT.rar`.
* **Header Security Checks:** Both **SPF (Sender Policy Framework)** and **DKIM (DomainKeys Identified Mail)** checks failed, indicating explicit email spoofing.

#### ⚙️ SOC Lifecycle Actions Taken:
1. **Assign:** Assigned the alert entry to myself inside the SOC platform dashboard.
2. **Triage:** Changed the ticket status dropdown from **New** ➡️ **In Progress**.
3. **Analyst Comment:** Inputted the summary analysis detailing the security check failures and attachment name.

### 📝 Task Answers & Flags
* What email address did the attacker spoof to send the phishing email?
  `support@microsoft.com`
* What flag did you receive after submitting the 5 Ws report and updating the status?
  `THM{nice_attempt_faking_microsoft_support}`

---

## 📈 Task 4: Escalation Guide

### 📖 Key Concepts
An L1 analyst scales their findings to a Level 2 (L2) or Tier 2 analyst when an incident exceeds pre-defined playbooks. Valid reasons for escalation include:
* Critical network asset compromise.
* Active ransomware or malware execution verified on an endpoint.
* Complex web-shell or advanced persistence mechanics requiring deep forensics.

#### ⚙️ Scenario 1 Checklist (Phishing Escalation):
* **L2 Escalation Target:** `E. Fleming` (Tier 2 SOC Lead)
* **Escalation Context:** User interacted with the attachment or the payload executed, demanding immediate host containment and network isolation.

#### ⚙️ Scenario 2 Checklist (Webshell Detection):
* **Indicator:** Exploit logs showing a suspicious command execution file dropped into an older Microsoft Exchange server web directory.

### 📝 Task Answers & Flags
* Which L2 analyst did you escalate the phishing alert to?
  `E. Fleming`
* What flag did you receive after correctly escalating your first alert?
  `THM{good_job_escalating_your_first_alert}`
* What flag did you receive after handling and reporting the second alert (web shell)?
  `THM{looks_like_webshell_via_old_exchange}`

---

## 📞 Task 5: SOC Communication

### 📖 Key Concepts
* **The Escalation Chain:** Standard operating procedures command reaching out upwards through the technical tier first. If L2 is unavailable, contact L3. Only reach out to higher management if upper engineering lines are completely exhausted or unresponsive.
* **Out-of-Band (OOB) Communications:** If corporate infrastructure (such as Slack, Microsoft Teams, or internal emails) is suspected of being compromised or monitored by an adversary, switch to verified external channels (e.g., secure cellular voice calls or out-of-network messaging tools).

### 📝 Task Answers & Flags
* Should you contact the security manager first if the Tier 2 analyst is unavailable? (Yea/Nay)
  `Nay`
* Should you contact the Tier 2 analyst if you realize a critical attack was missed? (Yea/Nay)
  `Yea`

---

## 🏆 Summary Checklist for SOC Analysts
* Always claim / change ticket status to **In Progress** *before* hunting artifacts.
* Keep **Analyst Comments** objective, objective-focused, and free of vague assumptions.
* Rely on the **5 Ws template** to maintain consistency across shift handovers.
