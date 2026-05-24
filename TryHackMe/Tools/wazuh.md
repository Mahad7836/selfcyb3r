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

## Important

- Select **Global Tenant**
- Wait several minutes after deployment
- `"Kibana server is not ready yet"` = normal startup delay

---

# Wazuh Agents

## Purpose

Agents monitor:

- Authentication attempts
- User management
- Processes
- File changes
- Security events

## Agent Deployment Requirements

Need:

- OS type
- Wazuh manager IP/DNS

---

# Policy Auditing

## Frameworks Supported

Wazuh audits systems against:

- MITRE
- NIST
- PCI DSS
- HIPAA
- GDPR
- CIS benchmarks

---

# Monitoring Logons

## Important Rule

### Rule ID 5710

Detects:

- Failed SSH login attempts

## Useful Fields

| Field | Description |
|---|---|
| `agent.ip` | IP of affected host |
| `agent.name` | Hostname |
| `rule.id` | Detection rule |
| `rule.description` | Event explanation |

---

# Sysmon Integration

## What is Sysmon?

Sysmon is a Windows monitoring tool from Sysinternals.

Used for:

- Process monitoring
- Registry monitoring
- Network connection logging
- DLL monitoring

---

# Important Sysmon Events

| Event ID | Description |
|---|---|
| 1 | Process creation |
| 3 | Network connection |
| 7 | DLL loaded |
| 8 | Remote thread creation |
| 11 | File creation |
| 13 | Registry modification |

---

# Sysmon Installation

```powershell
Sysmon64.exe -accepteula -i detect_powershell.xml
```

---

# Apache Log Monitoring

## Wazuh Localfile Config

```xml
<localfile>
  <location>/var/log/example.log</location>
  <log_format>syslog</log_format>
</localfile>
```

---

# Wazuh Rules

## Rules Location

```bash
/var/ossec/ruleset/rules
```

Contains:

- Detection rules
- Correlation logic
- Alert definitions

---

# Linux Auditing with auditd

## What is auditd?

Linux auditing framework for:

- Command execution tracking
- Syscall auditing
- User activity monitoring

---

# auditd Rules File

```bash
/etc/audit/rules.d/audit.rules
```

---

# Example auditd Rule

Monitor root command execution:

```bash
-a exit,always -F arch=b64 -F euid=0 -S execve -k audit-wazuh-c
```

---

# Load auditd Rules

```bash
sudo auditctl -R /etc/audit/rules.d/audit.rules
```

---

# Wazuh auditd Integration

Add to:

```bash
/var/ossec/etc/ossec.conf
```

Configuration:

```xml
<localfile>
  <location>/var/log/audit/audit.log</location>
  <log_format>audit</log_format>
</localfile>
```

---

# Wazuh API

## Purpose

Used to:

- Query manager
- Retrieve agent info
- Automate monitoring
- Execute management actions

---

# Authentication Example

```bash
curl -u wazuh:wazuh -k https://localhost:55000/security/user/authenticate?raw=true
```

---

# Get Manager Configuration

```bash
curl -k -X GET "https://MACHINE_IP:55000/manager/configuration?pretty=true&section=global" -H "Authorization: Bearer $TOKEN"
```

---

# Common HTTP Methods

| Method | Purpose |
|---|---|
| GET | Retrieve information |
| POST | Perform actions/create |
| PUT | Update |
| DELETE | Remove |

---

# Useful API Endpoint

```bash
/manager/info
```

Returns:

- Version
- Status
- Components

---

# Reporting

## Generate Reports

Path:

```txt
Modules → Security Events
```

Then:

- Select timeframe
- Generate PDF report

---

# Report Dashboard

Navigate:

```txt
Wazuh → Management → Reporting
```

---

# Sample Data

## Import Sample Data

Path:

```txt
Wazuh → Settings → Sample Data
```

Important:

- Use at least **Last 7 Days**
- Refresh dashboard after importing

---

# Important File Locations

| Purpose | Path |
|---|---|
| Wazuh rules | `/var/ossec/ruleset/rules` |
| Wazuh config | `/var/ossec/etc/ossec.conf` |
| auditd rules | `/etc/audit/rules.d/audit.rules` |
| auditd logs | `/var/log/audit/audit.log` |

---

# Important Commands

## Restart Wazuh Agent

```bash
sudo systemctl restart wazuh-agent
```

## Restart auditd

```bash
sudo systemctl restart auditd
```

## Load audit Rules

```bash
sudo auditctl -R /etc/audit/rules.d/audit.rules
```

---

# Key Takeaways

- Wazuh combines EDR + SIEM functionality
- Agents send logs to manager
- Sysmon improves Windows telemetry
- auditd improves Linux monitoring
- Rules define detections
- API enables automation
- Reporting simplifies analysis

---
