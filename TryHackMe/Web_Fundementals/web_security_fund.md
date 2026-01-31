# Web Security Fundamentals: Core Knowledge

A technical overview of web infrastructure components, the request-response cycle, and foundational security measures for applications, servers, and hosts.

---

## 1. Components of a Web Service
Every web service (e.g., tryhackme.com) relies on three primary layers. Security must be applied to all three to be effective.

| Component | Responsibility | Examples |
| :--- | :--- | :--- |
| **Application** | The front-end/back-end code, images, and logic. | HTML, CSS, JavaScript, PHP, Python |
| **Web Server** | Software that hosts the app and handles HTTP requests. | Apache, Nginx, IIS |
| **Host Machine** | The underlying Operating System (OS) and hardware. | Linux (Ubuntu/CentOS), Windows Server |

## 2. The Request-Response Cycle
The foundation of web communication is the **HTTP Protocol**.
* **Request:** The client (browser) asks for a resource (e.g., `GET /index.html`).
* **Response:** The server returns the resource and a status code (e.g., `200 OK`).
* **Security Risk:** Attackers can abuse this cycle by overwhelming servers (DoS) or injecting harmful commands into the request to trick the server.

## 3. Protecting the Application Layer
The application is often the most exposed part of the service.
* **Input Validation & Sanitization:** Ensuring all user input is safe before processing (prevents XSS and SQL Injection).
* **Secure Coding:** Avoiding insecure functions and ensuring detailed error messages are hidden from users.
* **Access Control:** Implementing the **Principle of Least Privilege** so users can only access data required for their specific role.

## 4. Protecting the Web Server Layer
The web server acts as the gateway between the user and the application code.
* **Logging:** Maintaining detailed access logs to track who is visiting and detect unusual patterns (e.g., repeated 404 errors indicating a directory brute-force).
* **Web Application Firewall (WAF):** A "bouncer" that inspects incoming traffic and blocks requests that match known attack signatures.
* **Content Delivery Network (CDN):** Hides the **Origin IP** of the server and absorbs DDoS traffic, providing a buffer between the user and the host.

## 5. Protecting the Host Machine
If the OS is compromised, the entire web service is lost regardless of how secure the app code is.
* **Least Privilege:** Running web services under low-privilege service accounts rather than `root` or `Administrator`.
* **System Hardening:** Disabling unnecessary services (like Telnet or FTP) and closing unused ports.
* **Patch Management:** Keeping the OS and all dependencies updated to protect against known exploits (CVEs).

## 6. Common Vulnerabilities (OWASP Top 10)
Basic security flaws frequently encountered in web applications:
* **Authentication Failure:** Weak passwords or lack of Multi-Factor Authentication (MFA).
* **Broken Access Control:** Allowing a user to access an admin panel or another user's data (e.g., IDOR).
* **Injection:** Tricking an application into executing unintended commands (SQLi, Command Injection).
* **Cryptographic Failures:** Transmitting sensitive data over unencrypted HTTP instead of HTTPS.

