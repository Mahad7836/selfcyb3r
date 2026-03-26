# TryHackMe Notes: Log Operations

This document covers the foundational concepts of what logs are, why they are critical for security operations, and how they are managed at scale within an enterprise environment.


# Log Operations

### 📌 Overview
Having logs is only the first step. **Log Operations** deals with how we collect, process, store, and analyze thousands of logs per second across an entire organization using a SIEM (Security Information and Event Management) system.



### 1. The Log Management Pipeline
To make logs useful for security analysts, they must flow through a specific pipeline:
1.  **Generation:** The endpoint, server, or firewall creates the log.
2.  **Collection & Forwarding:** Agents (like Winlogbeat, Filebeat, or Rsyslog) pick up the logs from the local machine and forward them to a central server.
3.  **Parsing & Normalization:** The SIEM breaks the log apart. *Normalization* is the critical step of converting different log formats into a single, standard schema (e.g., turning `src_ip`, `SourceIp`, and `IP_Address` all into a unified `source.ip` field).
4.  **Storage:** Logs are indexed and stored in a database (like Elasticsearch or Splunk indexers) so they can be searched quickly.
5.  **Analysis & Alerting:** Analysts query the logs, and automated rules trigger alerts if malicious patterns are detected.
6.  **Retention & Archiving:** Logs are kept "hot" (searchable) for a short period (e.g., 30-90 days) and then archived to cheaper, "cold" storage for compliance.

### 2. Log Collection Methods
* **Agent-Based:** Installing a lightweight piece of software on the endpoint (e.g., Elastic Beats, Splunk Universal Forwarder) to push logs to the SIEM. Good for deep OS-level visibility.
* **Agentless / Syslog Push:** Network devices (Firewalls, Routers) natively push their logs via the Syslog protocol (Port 514) to a centralized collector.
* **API Pull:** The SIEM reaches out to cloud services (like AWS CloudTrail, Office 365) via APIs to pull the logs down.

### 3. Common Log Operations Tools
| Tool | Function / Phase |
| :--- | :--- |
| **Rsyslog / Syslog-ng** | Linux log routing and forwarding daemons. |
| **Logstash / Fluentd** | Data processing pipelines (Parses and Normalizes logs). |
| **Elasticsearch / Splunk** | Log storage, indexing, and search engines (The core of the SIEM). |
| **Kibana / Splunk Web** | The front-end dashboard where analysts view logs and build graphs. |

### 💡 Key Takeaway for Analysts
In a SOC (Security Operations Center), **Normalization** is your best friend. Without it, you would have to write dozens of different queries to find the same type of attack across Windows, Linux, and Cisco devices.