# Intro to SIEM: Core Knowledge

A foundational overview of Security Information and Event Management (SIEM) systems, their architecture, and their role within a Security Operations Center (SOC).

---

## 1. What is SIEM?
SIEM is a security solution that provides a holistic view of an organization's IT security by collecting, aggregating, and analyzing data from various sources across the entire network.

It is a combination of two primary disciplines:
* **SIM (Security Information Management):** Focuses on the collection, storage, and long-term analysis of log data.
* **SEM (Security Event Management):** Focuses on real-time monitoring, correlation of events, and incident response.

## 2. The SIEM Workflow
The effectiveness of a SIEM depends on a structured data lifecycle:

1. **Log Collection:** Gathering raw logs from endpoints, servers, firewalls, and antivirus software.
2. **Data Ingestion/Parsing:** Converting raw, messy logs into a standardized format (Normalization) so the SIEM can "read" them consistently.
3. **Data Analysis:** Comparing normalized data against predefined "Correlation Rules."
4. **Alerting:** Notifying security analysts when a specific pattern (e.g., 50 failed logins in 1 minute) is detected.
5. **Dashboards:** Providing a visual representation of the network's security posture.

## 3. Capabilities of a SIEM
A SIEM isn't just a log storage bin; it provides active defense capabilities:

* **Real-time Monitoring:** Seeing events as they happen across the globe or the office.
* **Correlation Rules:** Connecting unrelated events. 
    * *Example:* An "Access Denied" log followed by a "Successful Admin Login" from an unusual IP triggers an alert.
* **Threat Intelligence:** Integrating feeds of known malicious IPs, domains, and file hashes to automatically flag threats.
* **Compliance:** Automating the reports needed for standards like PCI-DSS, HIPAA, or GDPR.

## 4. Common SIEM Solutions
Different organizations use different tools based on scale and budget:

| Tool | Focus |
| :--- | :--- |
| **Splunk** | Industry leader, highly powerful for both security and data analytics. |
| **ELK Stack** | (Elasticsearch, Logstash, Kibana) - A popular open-source alternative. |
| **Microsoft Sentinel** | A cloud-native SIEM/SOAR designed for Azure environments. |
| **IBM QRadar** | Known for advanced AI-driven correlation and massive scale. |

## 5. Why SIEM Matters for SOC Analysts
Without a SIEM, an analyst would have to log into every individual server and firewall to check for attacks. The SIEM acts as the **"Brain"** of the SOC, centralizing the visibility so that an analyst can investigate an entire attack chain from a single screen.

---
**Reference:** [TryHackMe - Intro to SIEM](https://tryhackme.com/room/introsiem)