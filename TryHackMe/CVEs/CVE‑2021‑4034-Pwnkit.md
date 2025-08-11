# Pwnkit (CVE-2021-4034)

🧠 Overview
Name: Pwnkit
Vulnerability: CVE-2021-4034 (Polkit - pkexec)
Type: Local Privilege Escalation (LPE)
Impact: Root access via misconfigured pkexec
Affected Systems: Most Linux distributions (Ubuntu, Debian, CentOS, etc.)

🛠️ Room Summary
Task 1: Introduction
Focus: Understanding and exploiting CVE-2021-4034

Exploit is local only, not remote.
Environment provided by THM via in-browser terminal or deployable VM.

Task 2: Background
pkexec is a tool used to execute commands as another user (commonly root).
The vulnerability allows an attacker to manipulate how environment variables are handled when pkexec is run with no arguments.
Due to a bug, pkexec misparses arguments and reads from an out-of-bounds memory location, leading to overwriting the environment.

Task 3: Exploitation Steps
✅ Confirm pkexec exists:

which pkexec

✅ Compile the exploit:

gcc cve-2021-4034-poc.c -o exploit

✅ Run the exploit:
./exploit

🏁 If successful, you should get a root shell. Check:

whoami

🔐 Grab the flag:

cat /root/flag.txt

Task 4: Mitigation
🔧 Update system packages:

sudo apt update && sudo apt upgrade

🛑 Temporary fix (remove SUID bit):

sudo chmod 0755 $(which pkexec)

✅ Check patched version:
A patched system will not escalate privileges when running the exploit; instead, pkexec will just show help output.