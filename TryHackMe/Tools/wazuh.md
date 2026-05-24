# Wazuh - TryHackMe Notes

Room: https://tryhackme.com/room/wazuhct

---

# Overview

## What is Wazuh?

Wazuh is an open-source security monitoring platform used for:

- Endpoint Detection & Response (EDR)
- SIEM capabilities
- Threat detection
- Log analysis
- File integrity monitoring
- Vulnerability detection
- Compliance auditing

Released in 2015.

---

# Architecture

## Wazuh Components

### Agent
A monitored device that:
- Collects logs
- Detects events
- Sends data to manager

Examples:
- Linux hosts
- Windows systems
- Servers

### Manager
Central server responsible for:
- Receiving logs
- Processing events
- Triggering alerts
- Managing agents

---

# Dashboard Access

Default THM credentials:

```txt
Username: wazuh
Password: eYa0M1-hG0e7rjGi-lRB2qGYVoonsG1K