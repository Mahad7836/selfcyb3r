# Windows Fundamentals 1: Core Knowledge

A technical summary of Windows OS architecture, navigation, and administrative utilities.

---

## 1. Operating System Overview
Windows is categorized into two main branches:
* **Workstation:** Designed for home/office use (Home, Pro, Enterprise).
* **Server:** Designed for hosting services, web apps, and domain management (Windows Server 2016/2019/2022).

## 2. File System Structure
The Windows file system uses a hierarchical structure starting from the `C:` drive. Understanding these paths is critical for enumeration.

| Directory | Description |
| :--- | :--- |
| `C:\Windows` | Contains the OS files and system drivers. |
| `C:\Windows\System32` | Critical directory for system DLLs and executables. |
| `C:\Users` | User profile folders (Desktop, Documents, AppData). |
| `C:\Program Files` | Default location for 64-bit applications. |
| `C:\Program Files (x86)` | Default location for 32-bit applications. |

## 3. The Run Command (`Win + R`)
The fastest way to access system utilities. Use these shortcuts to bypass the GUI menus:

| Command | Utility Launched |
| :--- | :--- |
| `control` | Control Panel |
| `taskmgr` | Task Manager |
| `msconfig` | System Configuration |
| `msinfo32` | System Information (Hardware/Software summary) |
| `resmon` | Resource Monitor |
| `cmd` | Command Prompt |
| `powershell` | Windows PowerShell |

## 4. Administrative Toolsets

### Task Manager (`Ctrl + Shift + Esc`)
* **Processes:** Monitor CPU, Memory, and Disk usage per app.
* **Performance:** Real-time graphs of system resources.
* **Startup:** Manage which applications launch automatically (critical for persistence checks).
* **Users:** See which users are currently logged into the system.

### Control Panel vs. Settings
* **Control Panel:** The "Legacy" interface. Necessary for advanced system settings, managing user accounts, and "Programs and Features" (to uninstall software).
* **Settings App:** The modern UI for Windows Updates, Personalization, and basic device management.

### System Properties
Accessed via `sysdm.cpl` or System settings. This provides:
* **Computer Name:** Essential for network identification.
* **Workgroup/Domain:** Identifies if the machine is part of an Active Directory environment.
* **System Specs:** Processor type and installed RAM.

## 5. File Explorer Configuration
For security auditing and CTFs, the following settings should be enabled in the **View** tab:
* **File name extensions:** Prevents masking malicious files (e.g., `script.ps1.txt`).
* **Hidden items:** Reveals files with the `hidden` attribute set by the OS or users.

