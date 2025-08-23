# Networking Concepts (TryHackMe – Cyber Security 101)

## 1. Introduction
   - Overview of IP addresses, packet journeys, and network fundamentals.
   - Part of a 4‑room sequence: Networking Concepts → Essentials → Core Protocols → Secure Protocols.

## 2. Learning Objectives
   - Understand the OSI model.
   - Learn about IP addresses, subnetting, and routing.
   - Use command-line tools to connect to open TCP ports. 

## 3. OSI Model (7 Layers)
   1. Physical – hardware transmission (cables, switches).
   2. Data Link – error‑free data transfer between nodes.
   3. Network – routing & IP addressing.
   4. Transport – reliable/unreliable data delivery (TCP/UDP).
   5. Session – session management between applications.
   6. Presentation – formatting, encryption, compression.
   7. Application – user‑facing protocols (HTTP, FTP, etc.).
   - Common Qs:
     • Layer 4 connects applications; Layer 3 handles routing; Layer 6 encodes data; Layer 2 transfers within a segment. 

## 4. TCP/IP Model (4 Layers)
   - Link (Physical + Data Link), Internet (Network), Transport, Application (combines OSI’s 5‑7). 
   - 
     • HTTP operates at the Application layer; TCP/IP Application layer spans 3 OSI layers. 

## 5. IP Addresses & Subnets
   - IPv4 addresses: e.g., 192.168.0.1 or 172.16.159.243. 
   - Checking network config:
     • Windows: `ipconfig`; Linux: `ifconfig` or `ip address show` (`ip a s`).
     • Example: IP 192.168.66.89, mask 255.255.255.0 (/24), broadcast 192.168.66.255. 
   - Subnetting: `/24` means first 24 bits shared across network; host range .1–.254; .0 = network, .255 = broadcast. {index=7}
   - Private IP ranges (RFC1918):
     • 10.0.0.0–10.255.255.255 (10/8)  
     • 172.16.0.0–172.31.255.255 (172.16/12)  
     • 192.168.0.0–192.168.255.255 (192.168/16). 
   - Example questions:
     • Non‑private IP: 49.69.147.197.  
     • Invalid IP: 192.168.305.19. 

## 6. UDP vs TCP
   - UDP: connectionless, fast, unreliable — e.g., ideal for streaming. 
   - TCP: connection‑oriented, reliable, uses three‑way handshake (SYN, SYN‑ACK, ACK); supports port numbers 1–65535. index=11}
   - Qs:
     • Three‑way handshake: TCP.  
     • Approx. number of ports: 65 000 (~65 thousand). 

## 7. Encapsulation
   - Data is encapsulated with headers (and trailers) as it moves down layers:
     • App data → Transport (TCP/UDP segment) → Network (IP packet) → Data‑link (Ethernet/WiFi frame).
   - Reversed upon reception to extract application data. 
   - Qs:
     • On WiFi, an IP packet is inside a **frame**.  
     • UDP encapsulation unit: **Datagram**.  
     • TCP: **Segment**. 

## 8. Telnet Usage
   - `telnet` is a TCP tool for remote communication (plaintext, insecure; largely replaced by SSH). 
   - Demo services on VM:
     • Echo server (port 7) – echoes input.  
     • Daytime server (port 13) – returns current date/time.  
     • Web server (port 80).
   - Examples:
     • Telnet to echo: sends “Hi” → receives “Hi”, etc.  
     • Telnet to daytime: returns e.g. “Thu Jun 20 12:36:32 PM UTC 2024” then disconnects.  
     • Telnet to HTTP: send `GET / HTTP/1.1` + `Host: ...`, gets response (e.g. lighttpd/1.4.63 and flag THM{TELNET_MASTER}). 