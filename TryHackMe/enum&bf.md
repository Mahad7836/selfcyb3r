# TryHackMe - Enumeration & Brute Force

## Overview

Enumeration is the process of gathering information about a target before attempting exploitation. In authentication systems, enumeration helps identify valid users, emails, reset tokens, and authentication weaknesses that can later be abused through brute-force attacks.

**Key Principle:**

> Enumeration first, brute force second.

---

# Authentication Enumeration

## What is Authentication Enumeration?

Authentication enumeration occurs when an application reveals different responses depending on whether a username/email exists.

### Example

Invalid email:

```text
Email does not exist
```

Valid email + wrong password:

```text
Invalid password
```

The difference allows attackers to identify registered users.

---

## Why It Is Dangerous

Attackers can:

* Discover valid usernames
* Build target lists
* Launch password attacks only against existing accounts
* Reduce brute-force time significantly

---

## Enumeration Workflow

1. Identify login page.
2. Test random email.
3. Compare error messages.
4. Determine if responses differ.
5. Automate the process.
6. Generate a list of valid users.

---

## Automation

Python's `requests` library can:

* Send POST requests
* Check responses
* Detect valid accounts
* Automate email enumeration

Common approach:

```python
requests.post()
```

Check response message:

```python
if "Email does not exist" in response:
```

Otherwise:

```python
Valid user found
```

---

# Password Reset Vulnerabilities

## Common Reset Methods

### Email-Based Reset

User receives:

* Reset link
* Reset token

Risk:

* Predictable tokens
* Token leakage
* Long token validity

---

### Security Questions

Examples:

* Mother's maiden name
* Favorite pet

Risk:

* OSINT
* Social media exposure
* Easily guessed answers

---

### SMS Reset

User receives OTP via SMS.

Risk:

* SIM swapping
* Message interception

---

# Predictable Token Attack

## Vulnerability

Application generates weak reset tokens.

Example:

```text
123
124
125
```

or

```text
100-999
```

A 3-digit token only has:

```text
900 possibilities
```

which is easily brute-forced.

---

## Attack Process

1. Request password reset.
2. Capture reset request.
3. Send to Burp Intruder.
4. Brute-force token values.
5. Find successful response.
6. Reset password.
7. Log in as victim.

---

## Generating Token Wordlists

Using Crunch:

```bash
crunch 3 3 -o otp.txt -t %%% -s 100 -e 200
```

Explanation:

| Option | Meaning         |
| ------ | --------------- |
| 3 3    | Length = 3      |
| -o     | Output file     |
| -t %%% | Numeric pattern |
| -s     | Start value     |
| -e     | End value       |

---

# Burp Suite Intruder

## Purpose

Automates repetitive requests.

Useful for:

* Username enumeration
* Password attacks
* Token brute forcing
* OTP attacks

---

## Basic Workflow

1. Capture request.
2. Send to Intruder.
3. Select attack position.
4. Load payload list.
5. Start attack.
6. Analyze responses.

---

## Indicators of Success

Look for:

* Different status code
* Different response size
* Different response body
* Redirects

Example:

```text
200 OK
```

instead of:

```text
401 Unauthorized
```

---

# HTTP Basic Authentication

## Authentication Header

Format:

```http
Authorization: Basic <base64>
```

Credentials:

```text
username:password
```

Encoded with Base64.

Example:

```text
admin:password123
```

Becomes:

```text
YWRtaW46cGFzc3dvcmQxMjM=
```

---

## Why It Is Weak

Base64 is:

* Encoding
* Not encryption

Anyone can decode:

```bash
echo "YWRtaW46cGFzc3dvcmQxMjM=" | base64 -d
```

Result:

```text
admin:password123
```

---

# Brute Forcing Basic Authentication

## Using Burp Intruder

### Steps

1. Capture Authorization header.
2. Decode Base64.
3. Highlight password field.
4. Load wordlist.
5. Add payload processing rules:

   * Prefix username
   * Re-encode Base64
6. Launch attack.

---

## Success Indicator

Look for:

```text
HTTP 200
```

instead of:

```text
HTTP 401
```

---

# Hydra

Hydra is a fast command-line brute-force tool.

## HTTP Basic Authentication Example

```bash
hydra -l admin -P passwords.txt http-get://target
```

### Parameters

| Option   | Description   |
| -------- | ------------- |
| -l       | Username      |
| -P       | Password list |
| http-get | Service type  |

---

## Advantages Over Burp

* Faster
* Multithreaded
* Scriptable
* Better for large wordlists

---

# OSINT

## Open Source Intelligence

Gathering information from publicly available sources.

Examples:

* Search engines
* Archived websites
* GitHub
* Social media
* DNS records

---

# Wayback Machine

Internet Archive stores old versions of websites.

Useful for finding:

* Old pages
* Deleted files
* Hidden directories
* Backup files
* Exposed credentials

Website:

```text
https://archive.org/web/
```

---

## waybackurls Tool

Collects archived URLs automatically.

Example:

```bash
waybackurls example.com
```

Potential discoveries:

```text
/admin
/backup
/config
/old-login
```

---

# Google Dorking

Advanced search operators used to find sensitive information.

---

## Admin Panels

```text
site:example.com inurl:admin
```

---

## Passwords in Log Files

```text
filetype:log "password" site:example.com
```

---

## Backup Directories

```text
intitle:"index of" "backup" site:example.com
```

---

# Key Takeaways

## Enumeration

* Identify valid users.
* Analyze application responses.
* Look for verbose error messages.

## Brute Force

* Use only after successful enumeration.
* Target known usernames.
* Automate attacks using Burp or Hydra.

## Password Resets

* Predictable tokens are dangerous.
* Weak OTP implementations are easily brute-forced.

## Basic Authentication

* Base64 is not encryption.
* Weak passwords can be cracked quickly.

## OSINT

* Historical data matters.
* Wayback Machine can reveal forgotten assets.
* Google Dorks uncover exposed information.

---

# Tools Used

```text
Burp Suite
Hydra
Crunch
Python Requests
Waybackurls
Google Dorks
```

---

# Room Summary

This room demonstrates how attackers combine:

1. Authentication enumeration
2. User discovery
3. Password reset weaknesses
4. Token brute forcing
5. HTTP Basic Auth attacks
6. OSINT techniques

to compromise authentication mechanisms efficiently.

Always enumerate before brute forcing.
