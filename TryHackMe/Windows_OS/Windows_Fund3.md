# Windows Fundamentals 3: Security & Data Protection

A technical summary of built-in Windows security features, including threat protection, network security, and encryption.

---

## 1. Windows Updates
The primary mechanism for maintaining system integrity and patching vulnerabilities.
* **Function:** Delivers security patches, bug fixes, and feature updates.
* **Frequency:** "Patch Tuesday" (the second Tuesday of every month).
* **Key Concept:** Windows 10/11 makes updates mandatory after a certain postponement period to ensure critical vulnerabilities (like those used in Ransomware) are patched.

## 2. Windows Security (Built-in Defense)
A unified interface to manage different protection layers. 

### A. Virus & Threat Protection
* **Microsoft Defender Antivirus:** The default real-time scanner.
* **Scan Options:** * `Quick Scan`: Checks common folders where threats hide.
    * `Full Scan`: Checks every file and running program.
    * `Custom Scan`: Checks specific locations.
* **Real-time Protection:** Constantly monitors for malware trying to install or run.

### B. Firewall & Network Protection
A firewall acts as a "security guard" for network ports. Windows uses three distinct **Firewall Profiles**:
1. **Domain:** Active when the device is authenticated to a Corporate Domain Controller.
2. **Private:** Used for trusted home or work networks.
3. **Public:** Most restrictive; used for untrusted networks like airport or coffee shop Wi-Fi.

### C. App & Browser Control
* **Windows Defender SmartScreen:** Protects against phishing sites and malicious downloads.
* **Exploit Protection:** Built-in mitigations to prevent common memory-based attacks (like Buffer Overflows).

## 3. Device Security
Focuses on hardware-level protection to ensure the OS hasn't been tampered with.
* **Core Isolation (Memory Integrity):** Uses virtualization to protect high-security processes from malicious code injection.
* **Security Processor (TPM):** * **TPM (Trusted Platform Module):** A dedicated microchip on the motherboard that provides hardware-based encryption keys.
    * **Note:** Essential for secure boot and disk encryption.

## 4. BitLocker Drive Encryption
Full-disk encryption designed to protect data even if the physical drive is stolen.
* **Requirement:** Ideally requires a **TPM 1.2+** to store keys.
* **Workaround:** If a machine lacks a TPM, a **USB Startup Key** must be inserted during boot to unlock the drive.

## 5. Volume Shadow Copy Service (VSS)
A feature that creates "snapshots" or point-in-time copies of files, even while they are in use.
* **System Restore:** Uses VSS to create **Restore Points** to roll back the OS after a bad update or driver install.
* **Security Warning:** Modern Ransomware often attempts to delete VSS snapshots first so that the user cannot restore their files without paying the ransom.

