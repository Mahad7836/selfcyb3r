# TryHackMe: SOC L2 Alert Triage Notes

## 📌 Executive Summary & Core Mindset
While **Level 1 (L1) analysts** focus on triage speed, initial validation, and alert volume, **Level 2 (L2) analysts** specialize in **triage quality**, deep log analysis, context building, and incident resolution. 

* **L1 Trigger:** A raw security alert.
* **L2 Trigger:** An escalated case, an urgent request from management, or direct customer escalations.
* **The Goal:** Build the complete attack chain, find the entry point (root cause), identify all Indicators of Compromise (IoCs), and mitigate the risk.

---

## 🏎️ Log Analysis Principles & Workflow

### 1. Understand the Detection Rule
* Never begin an investigation without fully grasping the **technique** or detection logic behind the rule.
* Focus entirely on **one case at a time** to prevent analytic fatigue and mixed contexts.

### 2. The Investigation Process (Story & Timeline)
* **Form a Narrative:** Formulate a high-level story of what happened (Why did this trigger? What launched it? What did it do next?).
* **Build Detailed Timelines:** Trace related actions chronologically (processes, files, networks, logs).
* **The Threat Hunting Loop:** Iterate through a continuous loop: Form a Hypothesis (Story) ➡️ Build Timeline to Fill Gaps ➡️ Refine/Change Story


---

## 👥 Verifying Ambiguous Activity
Before dropping the hammer on a critical infrastructure change, verify anomalies with stakeholders:
* **Users:** Confirm unusual logins or VPN locations directly (e.g., Proton VPN usage). If uncontactable during high-risk alerts, provisionally disable the account.
* **IT Support:** Validate unexpected administrative user creations or custom debugging tools.
* **DevOps:** Confirm unexpected API calls or script interactions.
* **Red Team:** Coordinate to confirm if the activity aligns with an internal active pentest.

---

## 🛡️ Response Matrix

| Incident Type | Core Action Steps |
| :--- | :--- |
| **True Positive (TP)** | 1. Isolate the affected host or account.<br>2. Remediate/remove persistent mechanisms.<br>3. Track the attack vector to prevent recurrence. |
| **Major Incidents** | **Prioritize Containment over Certainty**.<br>If active data exfiltration or ransomware is suspected, execute containment protocols (e.g., isolate endpoints) *before* finishing the multi-hour deep dive. |
| **False Positive (FP)** | 1. Suppress the immediate alert.<br>2. **Tune the underlying detection rule** to avoid future fatigue.<br>3. Document the reasoning cleanly. |

---

## 🏁 Case Resolution & Closing
A case is formally completed only when the threat is **fully eradicated and recovered**.
* **Evidence Preservation:** Document every step, script, and terminal output inside the ticketing platform.
* **Knowledge Sharing:** Brief the rest of the SOC team on newly discovered adversary behaviors.
* **Stakeholder Reporting:** Provide clear, executive-friendly status updates or formal reports to managers and clients.
