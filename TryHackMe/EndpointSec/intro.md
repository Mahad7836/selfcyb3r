# Intro to Endpoint Security: Core Knowledge

A technical summary of endpoint security monitoring, focusing on Windows process baselining, logging mechanisms, and investigation methodologies.

---

## 1. Endpoint Security Fundamentals
To identify malicious activity, a defender must first understand the "known good" state of an operating system.

### Core Windows Processes (The Baseline)
Standard Windows processes follow a strict parent-child hierarchy. Deviations from this often indicate process injection or masquerading. 



| Process | Parent Process | Description |
| :--- | :--- | :--- |
| **System** | None (Idle) | The kernel-mode process that manages system threads. |
| **smss.exe** | System | Session Manager Subsystem; responsible for starting user sessions. |
| **csrss.exe** | smss.exe | Client/Server Runtime Subsystem; manages windows and threads. |
| **wininit.exe** | smss.exe | Windows Initialization Process; starts services and `lsass`. |
| **services.exe** | wininit.exe | Service Control Manager; handles system services. |
| **svchost.exe** | services.exe | Host process for DLL-based services. |
| **lsass.exe** | wininit.exe | Local Security Authority Subsystem; enforces security policies. |
| **explorer.exe** | userinit.exe | The user shell (Taskbar, Desktop). |

### Sysinternals for Investigation
* **TCPView:** Displays all active TCP/UDP connections and resolves IPs to domains.
* **Process Explorer:** Shows process hierarchies, loaded DLLs, and file handles.

## 2. Endpoint Logging and Monitoring
### Windows Event Logs
Stored in `.evtx` format at `C:\Windows\System32\winevt\Logs`. Accessed via Event Viewer, `wevtutil.exe`, or PowerShell.

### Sysmon (System Monitor)
Advanced system service that logs high-detail activity:
* **Event ID 1:** Process Creation (includes command-line arguments).
* **Event ID 3:** Network Connections.
* **Event ID 7:** Image Loaded (detects DLL injection).

### OSQuery & Wazuh
* **OSQuery:** Exposes an OS as a relational database for SQL-based querying.
* **Wazuh (EDR):** A unified platform that uses agents to monitor endpoints for suspicious activity and provides centralized visualization.

## 3. Investigation Methodology
* **Baselining:** Defining "normal" behavior (e.g., authorized software, typical user hours).
* **Event Correlation:** Connecting data from multiple sources (Firewall + Sysmon) to build an attack timeline.

---
**Reference:** [TryHackMe - Intro to Endpoint Security](https://tryhackme.com/room/introtoendpointsecurity)