Overview & Objectives

What vulnerabilities are, why they matter.
How vulnerabilities are rated (CVSS & VPR).
Key databases (like NVD & Exploit-DB) for researching vulnerabilities.


🧩Types of Vulnerabilities
Definition: A vulnerability is a weakness in the design, implementation, or behavior of a system or application that can be exploited to access unauthorized info or perform unauthorized actions (NIST definition) .

Five main categories:

Operating System – often leads to privilege escalation
(Mis)Configuration‑Based – insecure default or wrong settings
Weak or Default Credentials – easily guessed or known credentials
Application Logic – flaws in business/auth logic
Human‑Factor – social engineering, phishing 


Questions & Answers:

Upgrading from user to administrator → Operating System
Bypassing login via cookie manipulation → Application Logic 


📊CVSS vs VPR

CVSS (Common Vulnerability Scoring System)
First published in 2005
Scores based on exploitability, impact, availability of exploits, CIA triad, etc.
Produces severity categories from None up to Critical
Advantages: free, widely adopted (e.g. by NIST); limitation: static scoring, doesn’t consider real‑world risk dynamics 

VPR (Vulnerability Priority Rating)
Developed by Tenable
Prioritizes real-world risk—use of software by the organization, exploit availability, time decay
Scores are dynamic and risk‑based, lacking a “None/Informational” tier
Not open‑source / proprietary; doesn’t follow CIA triad metrics


📚Vulnerability Databases

Two crucial resources:

NVD (National Vulnerability Database): official repository of public CVEs. Example: 1585 CVEs published in July 2021 .
Exploit‑DB: maintained by Offensive Security, houses proof-of-concepts and exploit code tied to specific vulnerabilities and versions .


| Topic                    | Key Takeaways                                                                |
| ------------------------ | ---------------------------------------------------------------------------- |
| Vulnerability Definition | Flaw or weakness in system/app design, implementation, or behavior           |
| Vulnerability Categories | OS, misconfiguration, weak credentials, app logic, human-factor              |
| CVSS                     | First published 2005; free; static scoring                                   |
| VPR                      | Risk-based, dynamic scoring; proprietary                                     |
| Databases                | NVD (CVE tracking); Exploit‑DB (exploit PoCs); author: Offensive Security    |
| Version Disclosure       | Reveals version; enables targeted exploit searches                           |
| ACKme Exploit Showcase   | Found version → found exploit → reverse shell → flag: THM{ACKME\_ENGAGEMENT} |
