1. What Is SQL Injection? 
Injection occurs when a web app uses unsanitized user inputs in SQL queries, allowing attackers to inject malicious SQL.
Results can include authentication bypass, data exfiltration, schema discovery, or server takeover depending on DBMS privileges. 


2. Common Attack Techniques
a) Authentication Bypass

Use payloads like:
' OR 1=1-- 

This makes the query always true and comments out the rest, bypassing login checks. 

b) Error-Based Injection
Trigger an error (e.g., unclosed quote) to reveal DB structure or data in the error message. Useful for initial reconnaissance. 


c) Union-Based Injection
Discover columns count via trial-and-error on UNION SELECT 1,2...?

Then use UNION SELECT 1,2,database() or group_concat(...) to extract schema/data. 

d) Boolean-Based Blind
Use conditions like AND (SELECT LENGTH(password) FROM users WHERE username='admin') > 5. The page response (true/false) leaks info bit-by-bit. 

e) Time-Based Blind
Inject time delays, e.g.:

' OR IF(database() LIKE 'u%', SLEEP(5), 0)-- 
and check response delay to infer truth. 


f) Out-of-Band (OOB)
Trigger the DB to make network backcalls (DNS/HTTP) to attacker-controlled hosts, exfiltrating data without page changes. 


3. Practical Enumeration Workflow
Detect vulnerability with simple payloads: ', OR 1=1--, time-delay tests, or ORDER BY n. 

Count columns using UNION SELECT incrementally. 

Extract schema:

Use UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = database()

Then group_concat(column_name) from information_schema.columns. 

Extract data: e.g., group_concat(username,':',password). 

Use boolean/time blind if no visible output or union is blocked. 

4. Tools:
sqlmap automates detection & exploitation, though manual techniques are crucial (e.g. against WAFs). 
Burp Suite / intercepting proxies help inject payloads into GET/POST/headers. 
SQLmap- to do sqli

5. Mitigation Strategies

-Use Prepared Statements (parameterized queries) to separate code from data. 
-Validate & sanitize inputs (whitelisting) to disallow dangerous characters. 
-Escape inputs when parameterization isn't possible. 
-Least privilege principle: DB users should have minimal needed permissions. 
-Use Web Application Firewalls (WAFs) to block common SQLi patterns. 
-Regular auditing & pen-testing, including automated and manual scans. 
-Keep DBMS/software patched to avoid known exploits. 

6. Why It Matters
Still widespread: ~6.7% of open-source and 10% of closed-source vulnerabilities are SQLi, with rising CVEs as recently as 2024. 

Highly impactful: The MOVEit breach in 2023 exploited SQLi, illustrating real-world consequences. 



| Attack Type      | Example Payload               | Purpose                             |
| ---------------- | ----------------------------- | ----------------------------------- |
| Auth Bypass      | `' OR 1=1--`                  | Login bypass                        |
| Error-Based      | `'` / `UNION SELECT`          | Schema discovery via errors         |
| Union-Based      | `UNION SELECT 1,2,database()` | Pull database name                  |
| Boolean Blind    | `AND (LENGTH(password)>5)`    | Inference from true/false           |
| Time-Based Blind | `IF(..., SLEEP(5), 0)`        | Inference via response delay        |
| OOB Injection    | `...; CALL DNS...`            | Exfiltration via external callbacks |
