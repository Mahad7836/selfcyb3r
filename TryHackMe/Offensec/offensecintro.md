Offensive Security: Intro Room on THM (TryHackMe) - A Comprehensive Guide

1. Reconnaissance using Gobuster
In cybersecurity, reconnaissance or information gathering is an essential phase. Gobuster is a tool used to discover hidden directories and files on a web server through brute-forcing. It is used commonly in penetration testing to identify potential vulnerabilities.

Command:

gobuster -u http://fakebank.thm -w wordlist.txt dir

Explanation:

-u: Specifies the URL (target) to scan.

-w: Provides the path to a wordlist that contains common directory or file names.

dir: Instructs Gobuster to look for directories.

