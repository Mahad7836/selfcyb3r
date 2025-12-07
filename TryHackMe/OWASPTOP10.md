# OWASP Top 10 (2021) Notes

The OWASP Top 10 is a standard awareness document for developers and web application security, representing the most critical security risks to web applications.

## A01:2021 - Broken Access Control
Occurs when users can act outside of their intended permissions. This includes accessing other users' accounts (Horizontal Privilege Escalation) or gaining admin rights (Vertical Privilege Escalation).

Common Vulnerabilities
IDOR (Insecure Direct Object References): Accessing objects (files, database records) by simply changing an ID parameter in the URL.

Path Traversal: Accessing files outside the web root (e.g., ../../etc/passwd).

Practical (IDOR Challenge)
Scenario: Change the note_id parameter in the URL to access another user's note.

## A02:2021 - Cryptographic Failures
Previously "Sensitive Data Exposure". Focuses on failures related to cryptography (or lack thereof), leading to exposure of sensitive data like passwords, credit card numbers, etc.

Key Concepts
Weak Algorithms: Using MD5 or SHA1 instead of stronger hashes like SHA-256 or bcrypt.

Hardcoded Keys: Storing encryption keys directly in the source code.

Plaintext Transmission: Sending sensitive data over HTTP instead of HTTPS.

## A03:2021 - Injection
Occurs when untrusted data is sent to an interpreter as part of a command or query.

Types
SQL Injection (SQLi): Manipulating database queries.

Command Injection (OS Injection): Executing system commands via the web application (e.g., adding ; ls -la to an input).

Practical (Command Injection)
Strange File: drpepper.txt

## A04:2021 - Insecure Design
A new category for 2021. Focuses on risks related to design flaws and architectural structures rather than implementation bugs. "You cannot fix insecure design with perfect coding."

Examples
Logic Flaws: Resetting a password without verifying the old one properly.

Lack of Rate Limiting: Allowing unlimited login attempts.

## A05:2021 - Security Misconfiguration
One of the most common issues. Includes default configurations, incomplete configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages.

Key Checks
Change default passwords.

Disable directory listing.

Remove debugging features in production.

## A06:2021 - Vulnerable and Outdated Components
Using libraries, frameworks, or other software modules with known vulnerabilities.

Mitigation
Maintain a Software Bill of Materials (SBOM).

Regularly scan dependencies (e.g., npm audit, OWASP Dependency Check).

## A07:2021 - Identification and Authentication Failures
Previously "Broken Authentication". Issues allowing attackers to compromise passwords, keys, or session tokens.

Common Attacks
Brute Force: Guessing passwords.

Credential Stuffing: Using stolen credentials from one breach to log into another service.

Session Hijacking: Stealing a valid session ID.

## A08:2021 - Software and Data Integrity Failures
Focuses on making assumptions related to software updates, critical data, and CI/CD pipelines without verifying integrity.

Examples
Insecure Deserialization (trusting serialized objects).

Installing software updates without verifying digital signatures.

## A09:2021 - Security Logging and Monitoring Failures
Failures to log critical events (logins, failed transactions) or monitor logs for suspicious activity, allowing breaches to go undetected.

Best Practices
Log all login failures and access control failures.

Ensure logs cannot be modified by attackers.

Use a SIEM tool to aggregate and analyze logs.

## A10:2021 - Server-Side Request Forgery (SSRF)
Occurs when a web application is induced to make a request to a URL supplied by the user. This allows attackers to access internal services (like cloud metadata APIs or local admins) that are not exposed to the internet.

Types
Regular SSRF: Data is returned to the attacker.

Blind SSRF: The request is made, but no data is returned (exploit via timing or error messages).
