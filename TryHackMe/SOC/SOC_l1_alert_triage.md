# TryHackMe: SOC L1 Alert Triage Room Notes

## Room Overview
This room focuses on triaging security alerts in a Security Operations Center (SOC) environment, analyzing alert details, determining the severity and verdict (True Positive vs. False Positive), and closing them with appropriate documentation.

---

## Executive Summary of Flags
* **First-Priority Alert Flag:** `THM{phishing_by_another_name}`
* **Second-Priority Alert Flag:** `THM{macro_or_no_macro_that_is_the_question}`
* **Third-Priority Alert Flag:** `THM{should_we_allow_github_for_devs?}`

---

## Complete Alert Walkthroughs

### 1. First-Priority Alert: Potential Phishing / Malicious Attachment
* **Alert Details:** High-severity alert involving an inbound email containing a suspicious attachment or link targeting an internal user.
* **Analysis & Verification:**
  * Inspect sender domain reputation and email headers.
  * Analyze attachment hash via Open Source Intelligence (OSINT) tools like VirusTotal.
  * Identify malicious macros or harvesting links embedded in the document.
* **Verdict:** **True Positive (TP)**
* **Remediation Steps:**
  1. Assign the alert to yourself.
  2. Document the threat vectors and indicators of compromise (IoCs).
  3. Isolate the affected host or block the sender domain.
  4. Close the alert to reveal the flag: `THM{phishing_by_another_name}`

### 2. Second-Priority Alert: Malicious Document / Macro Execution
* **Alert Details:** Medium-severity alert triggered by a Microsoft Office application spawning an anomalous child process (e.g., `cmd.exe` or `powershell.exe`).
* **Analysis & Verification:**
  * Evaluate the process command line parameters.
  * Look for obfuscated scripts or unauthorized network connections initiated by the payload.
* **Verdict:** **True Positive (TP)**
* **Remediation Steps:**
  1. Assign the alert to yourself.
  2. Document the exact malicious command executed by the process tree.
  3. Change status to resolved.
  4. Close the alert to reveal the flag: `THM{macro_or_no_macro_that_is_the_question}`

### 3. Third-Priority Alert: Download from GitHub Repository
* **Alert Details:** Low-severity alert flags an employee downloading resources directly from a public GitHub repository.
* **Analysis & Verification:**
  * Cross-reference the destination user asset with organizational roles.
  * The user belongs to the **Software Development / Engineering** organizational unit.
  * Developers routinely clone, download, and audit code from repository hosting platforms like GitHub.
* **Verdict:** **False Positive (FP)** (Benign / Authorized business activity)
* **Remediation Steps:**
  1. Assign the alert to yourself.
  2. Document that the user is authorized to use GitHub for official development work.
  3. Close the alert as a False Positive to reveal the flag: `THM{should_we_allow_github_for_devs?}`

---

## Core SOC Triage Methodology
1. **Ownership:** Always assign the alert to your analyst profile first to avoid split work.
2. **Context Gathering:** Correlate user departments, baseline activities, and known normal processes before escalating.
3. **Documentation:** Write objective notes capturing the *who, what, where, and why* before marking an alert resolved.
