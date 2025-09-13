===========================
NMAP - TryHackMe Room Notes
===========================

🔹 BASIC SCANS
-------------
1. Simple Scan:
   nmap [IP]

2. Service Version Detection:
   nmap -sV [IP]

3. Operating System Detection:
   nmap -O [IP]

4. All in One (Aggressive Scan):
   nmap -A [IP]

5. Scan Specific Ports:
   nmap -p 22,80,443 [IP]

6. Scan All Ports (1-65535):
   nmap -p- [IP]

7. Fast Scan (Top 100 ports):
   nmap -F [IP]

🔹 OUTPUT OPTIONS
-----------------
1. Save Output to File:
   nmap -oN output.txt [IP]

2. Save All Formats:
   nmap -oA scan_results [IP]

🔹 STEALTH & EVASION
---------------------
1. SYN Scan (Stealth):
   nmap -sS [IP]

2. UDP Scan:
   nmap -sU [IP]

3. Fragment Packets:
   nmap -f [IP]

4. Decoy Scan:
   nmap -D RND:10 [IP]

5. Spoof MAC Address:
   nmap --spoof-mac Apple [IP]

6. Set Timing (0-5, slower to faster):
   nmap -T4 [IP]

🔹 SCRIPTING & ENUMERATION
---------------------------
1. Use Default Scripts:
   nmap -sC [IP]

2. Use Specific NSE Script:
   nmap --script=http-title [IP]

3. Script + Version:
   nmap -sC -sV [IP]

4. Vulnerability Scripts:
   nmap --script vuln [IP]

🔹 HOST DISCOVERY
------------------
1. Ping Scan:
   nmap -sn [IP]

2. Disable DNS Resolution:
   nmap -n [IP]

3. Scan a Range:
   nmap 192.168.1.0/24

🔹 COMMON NSE SCRIPTS
----------------------
- http-title
- http-enum
- ftp-anon
- smb-enum-shares
- smb-enum-users
- ssh-auth-methods
- ssl-cert
- dns-zone-transfer

🔹 EXAMPLES
------------
1. Full Aggressive Scan:
   nmap -A -T4 [IP]

2. Full TCP Port Scan with Service Detection:
   nmap -p- -sV -T4 [IP]

3. UDP & TCP Scan:
   nmap -sS -sU -T4 -p T:1-65535,U:1-100 [IP]

===========================
