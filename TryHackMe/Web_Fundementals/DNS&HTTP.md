# 🧠 TryHackMe - DNS and HTTP Deep Dive Notes

This markdown file summarizes the key takeaways and learning points from two foundational TryHackMe rooms: **DNS in Detail** and **HTTP in Detail**.

---

## 🌐 Room 1: DNS in Detail

### ✅ Core Concepts
- **DNS** stands for Domain Name System – it's the phonebook of the internet.
- Converts domain names (e.g., `google.com`) into IP addresses.
- **DNS Record Types**:
  - `A`: Maps domain to IPv4 address
  - `AAAA`: Maps domain to IPv6 address
  - `CNAME`: Alias for another domain
  - `MX`: Mail exchange record (for email)
  - `TXT`: Used for SPF, DKIM, verification, etc.

### 📡 DNS Resolution Process
1. Client queries recursive resolver (usually your ISP or internal DNS).
2. Resolver queries root → TLD → authoritative DNS.
3. Final IP is returned to the client and cached.

### 🔐 Security Concepts
- DNS Spoofing / Poisoning
- DNS over HTTPS (DoH)
- DNSSEC (Domain Name System Security Extensions)

### 🛠️ Tools/Commands
- `nslookup`, `dig`, `host`
- Example: `dig google.com ANY`

---

## 🌐 Room 2: HTTP in Detail

### ✅ Core Concepts
- **HTTP (HyperText Transfer Protocol)** is a stateless, application-layer protocol.
- Follows **request → response** model.
- Used for communication between browsers and web servers.

### 🧱 HTTP Structure
- **Request Line**: `GET /index.html HTTP/1.1`
- **Headers**: `Host`, `User-Agent`, `Cookie`, etc.
- **Body** (optional): Sent with `POST` requests

### 📤 Methods
- `GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`

### 🔐 Status Codes
- `1xx`: Informational
- `2xx`: Success (200 OK)
- `3xx`: Redirection (301, 302)
- `4xx`: Client Errors (404 Not Found)
- `5xx`: Server Errors (500 Internal Error)

### 📦 Cookies & Sessions
- Cookies are stored on the client side, sent with every request.
- Sessions managed using server-side identifiers.

### 🛠️ Tools Used
- Browser DevTools
- `curl`, `Burp Suite`

### 💡 Key Takeaways
- HTTP is inherently insecure (use HTTPS)
- Understand request-response flow to exploit/investigate web vulns

---

## ✍️ Notes
These notes are compiled from memory after completing the rooms. Lab steps were not recorded. This file serves as a high-level concept refresher.
