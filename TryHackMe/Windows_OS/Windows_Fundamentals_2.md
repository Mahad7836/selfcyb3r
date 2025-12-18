# Windows Fundamentals 2: System Management & Internal Mechanics

A technical deep-dive into Windows administration tools, resource monitoring, and the configuration registry.

---

## 1. System Configuration (`msconfig`)
`msconfig` is a legacy tool primarily used for advanced troubleshooting and managing the boot process.

| Tab | Purpose |
| :--- | :--- |
| **General** | Select startup modes (Normal, Diagnostic, Selective). |
| **Boot** | Configure Safe Mode options and boot timeout settings. |
| **Services** | Enable/Disable background services (useful for finding non-Microsoft persistence). |
| **Startup** | Links to Task Manager to manage auto-start applications. |
| **Tools** | A "hub" for launching other administrative tools (Event Viewer, Command Prompt, etc.). |

## 2. Computer Management (`compmgmt.msc`)
A "Consolidated Console" that groups several critical MMC (Microsoft Management Console) snap-ins into one interface.

### A. System Tools
* **Task Scheduler:** Automates tasks/scripts based on triggers (time, logon, or event).
* **Event Viewer:** The OS "Audit Trail."
    * **Application:** Logs from software installed on the system.
    * **Security:** Logs login attempts, file access, and policy changes.
    * **System:** Logs OS-level events (driver failures, updates).
* **Shared Folders:** View all network shares and see who is currently connected to your machine via the network.

### B. Storage
* **Disk Management:** Used for initializing new disks, creating partitions, and changing drive letters.

### C. Services and Applications
* **Services:** View the status (Running/Stopped) and Startup Type (Manual/Automatic/Disabled) of all system services.

## 3. Resource Monitoring & Performance
* **Resource Monitor (`resmon`):** Provides a more granular view than Task Manager. It allows you to monitor specific **File Handles** and **Network Connections** per process.
    * *Security Note:* If a suspicious process is running, use `resmon` to see exactly what files it is modifying or what IP addresses it is communicating with.
* **System Information (`msinfo32`):** A comprehensive summary of hardware and software environments, including **Environment Variables** (like `%PATH%`).

## 4. Windows Registry (`regedit`)
The Registry is a hierarchical database that stores configuration settings for the OS and applications. It is organized into five "Hives":

| Hive | Description |
| :--- | :--- |
| **HKEY_CLASSES_ROOT** | Information about file associations and OLE. |
| **HKEY_CURRENT_USER** | Settings specific to the user currently logged in. |
| **HKEY_LOCAL_MACHINE** | Settings for the hardware and OS (applies to all users). |
| **HKEY_USERS** | Contains all loaded user profiles. |
| **HKEY_CURRENT_CONFIG** | Hardware profile information used at system startup. |

> **Analogy:** If the File System is the "Body" of Windows, the Registry is the "Brain" (storing memories of how everything should behave).

## 5. User Account Control (UAC)
UAC is a security feature that prevents unauthorized changes to the OS. 
* It works by running most applications with **Standard User** privileges, even if you are an Administrator, until a prompt is accepted to "Elevate" the process.
* **UAC Settings:** Can be adjusted from "Always Notify" (most secure) to "Never Notify" (least secure/not recommended).

-