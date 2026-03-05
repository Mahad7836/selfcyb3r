# TryHackMe Notes: OWASP Top 10 2025 - IAAA Failures

## 📌 Room Overview
This room explores three key categories from the OWASP Top 10 (2025 list) that relate directly to the breakdown of the **IAAA** security model. By understanding how these components fail, you learn how threat actors bypass controls to access unauthorized data, hijack sessions, and evade detection.

---

## Task 2: What is IAAA?
IAAA is a sequential, foundational security model used to verify users and their actions within an application. Each step relies heavily on the previous one; you cannot skip a level. If one step is broken, the subsequent steps cannot function securely.



The four components are:
1. **Identity (Identification):** The unique account or claim (e.g., User ID, email, username) that represents a person or a service.
2. **Authentication:** The method used to prove that the identity is genuine (e.g., Passwords, OTPs, Biometrics, Passkeys).
3. **Authorisation:** The process of determining exactly what the authenticated identity is allowed to see or do within the application.
4. **Accountability:** The process of recording, auditing, and alerting on user actions (who did what, when, and from where).

---

## Task 3: A01 - Broken Access Control
**Broken Access Control** occurs when an application’s server does not properly enforce limitations on what authenticated users are allowed to do. The application implicitly trusts the client-side requests too much.

* **Key Concept - IDOR (Insecure Direct Object Reference):** A common access control vulnerability where a user can manipulate an input (like a URL parameter) to access other users' data.
  * *Example:* Changing `?accountID=7` to `?accountID=6` to view another user's private financial data.



**Types of Privilege Escalation:**
* **Horizontal Privilege Escalation:** Accessing data or resources belonging to another user who has the *same* role/permissions as you (e.g., User A reading User B's private messages).
* **Vertical Privilege Escalation:** Jumping to a higher-level role to perform unauthorized actions (e.g., a standard user accessing `/admin/delete_user`).

🛡️ **Remediation:** Always enforce strict server-side checks on *every* single request to verify the user has the explicit right to view the requested data or perform the requested action.

---

## Task 4: A07 - Authentication Failures
**Authentication Failures** happen when an application cannot reliably bind a user's identity securely, allowing an attacker to masquerade as another user.



**Common Issues & Vulnerabilities:**
* **Username Enumeration:** When an application's login or registration page gives different responses for valid vs. invalid usernames, allowing attackers to compile a list of valid accounts.
* **Weak Passwords & Rate Limiting:** Allowing easily guessable passwords combined with a lack of account lockouts or rate-limiting, which opens the door for brute-force and credential-stuffing attacks.
* **Logic Flaws:** Errors in the registration or password-reset flows. For example, if the system has an "admin" user, an attacker might register "aDmiN" to trick the backend database or application logic into granting them administrative rights.
* **Insecure Session Handling:** Utilizing predictable session cookies or failing to invalidate sessions upon logout.

---

## Task 5: A09 - Logging & Alerting Failures
This category represents a direct failure of the **Accountability** phase. When applications fail to log security-relevant events, defenders are rendered blind. They cannot detect active attacks or conduct post-incident forensic investigations.



**What Logging Failures Look Like:**
* Missing records of critical authentication events (e.g., failed logins, password changes, 2FA modifications).
* Logs that generate vague, unhelpful error messages without timestamps or IP addresses.
* Lack of real-time alerting for anomalies (e.g., a burst of brute-force attempts or sudden privilege elevations).
* Storing logs locally on the same host as the application, allowing an attacker to easily tamper with or delete them after a breach.

🛡️ **Remediation:** Log the entire authentication lifecycle. Centralize logs off-host using a SIEM (Security Information and Event Management) solution with strict retention policies. Configure automated alerts for behavioral anomalies.

---

## Task 6: Conclusion (Key Takeaways)
* Application security is a linear chain: **Identity → Authentication → Authorisation → Accountability**. 
* **A01 (Broken Access Control):** Never trust user input; validate permissions server-side.
* **A07 (Authentication Failures):** Secure your login logic, enforce strong session management, and prevent brute-forcing.
* **A09 (Logging & Alerting Failures):** Without centralized, detailed logs, you will never know if or when your application has been compromised.