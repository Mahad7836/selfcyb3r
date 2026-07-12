# Metasploit: The Basics — Core Knowledge

A technical summary of the Metasploit Framework (MSF), its architecture, core modules, and standard exploitation workflow.

---

## 1. Introduction to Metasploit
The Metasploit Framework is the world's most widely used penetration testing platform. It centralizes a massive database of known exploits, payloads, and post-exploitation tools, allowing security professionals to verify vulnerabilities and automate exploitation.

### Interface Types
* **msfconsole:** The primary, interactive command-line interface used by most practitioners.
* **msfvenom:** A standalone payload generator used to craft custom shellcode and executables for specific target environments.

## 2. Metasploit Architecture & Modules
Metasploit is highly modular. Every function is separated into a specific block of code known as a **module**.

| Module Type | Purpose | Key Sub-categories |
| :--- | :--- | :--- |
| **Exploit** | Code that leverages a vulnerability to execute a payload on a target system. | Windows, Linux, Web Applications |
| **Payload** | The code that runs on the target *after* a successful exploit (e.g., establishing a shell). | Singles, Stagers, Stages |
| **Auxiliary** | Tools used for scanning, enumeration, sniffing, and administrative tasks. No exploitation occurs. | Port Scanners, Fuzzers, Login Brute-forcers |
| **Post** | Gathers information, dumps hashes, and establishes persistence *after* a system is compromised. | Gather, Windows, Linux |
| **Encoder** | Alters the payload's signature to assist in bypassing basic signature-based Antivirus (AV) detection. | `shikata_ga_nai` |
| **NOPs** | (No Operation) Used to create padding in memory to ensure payload execution stability. | x86, x64 |
| **Evasion** | Modules designed to directly bypass host-based security controls (like Windows Defender). | — |

### Understanding Payloads: Staged vs. Inline (Singles)
* **Inline / Singles:** The entire payload (exploit + shellcode) is sent to the target in one single transmission. They are more stable but take up more space in memory.
    * *Syntax Indicator:* Separated by an underscore (`windows/meterpreter_reverse_tcp`).
* **Staged:** A small "stager" is sent first to open a connection. Once established, it downloads the larger "stage" payload into memory. Useful when memory buffer space is limited.
    * *Syntax Indicator:* Separated by a forward slash (`windows/meterpreter/reverse_tcp`).

## 3. Core Console Command Reference

### Exploration Commands
* `search [keyword]`: Finds modules related to a specific vulnerability, CVE, or software platform.
* `use [module_path]`: Selects a module to make it active.
* `info`: Displays detailed metadata about the active module (authors, options, target constraints, and CVE descriptions).
* `show options`: Displays the required variables for the active module.

### Variable Management
* `set [variable_name] [value]`: Sets a variable local to the current module.
* `setg [variable_name] [value]`: Sets a global variable across all modules (e.g., setting your attack machine IP via `setg LHOST`).
* `unset`: Clears a configured variable.

### Context Variables
* **RHOSTS:** Remote Host(s) — The target IP address, range, or CIDR network.
* **RPORT:** Remote Port — The target port running the vulnerable service.
* **LHOST:** Local Host — The IP address of your attacking machine (e.g., your TryHackMe VPN IP).
* **LPORT:** Local Port — The port on your attacking machine that will listen for the returning shell connection.

## 4. Standard Exploitation Workflow

The typical lifecycle of a Metasploit engagement follows a predictable structure:

```text
[Search for Exploit] ➔ [Select Module] ➔ [Configure RHOSTS/LHOST] ➔ [Verify Vulnerability via "check"] ➔ [Execute via "exploit" or "run"]