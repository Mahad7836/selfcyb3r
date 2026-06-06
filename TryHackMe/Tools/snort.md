# TryHackMe - Snort (SOC Level 1) Notes

## Overview

Snort is an open-source Network Intrusion Detection and Prevention System (IDS/IPS).

### Main Capabilities

* Real-time traffic analysis
* Packet logging
* Protocol analysis
* Intrusion detection
* Intrusion prevention
* Rule-based detection engine

---

# IDS vs IPS

## IDS (Intrusion Detection System)

Detects malicious activity and generates alerts.

### Types

#### HIDS (Host-Based IDS)

Monitors a single host/system.

#### NIDS (Network-Based IDS)

Monitors network traffic.

---

## IPS (Intrusion Prevention System)

Detects and actively blocks malicious activity.

### Types

#### HIPS (Host-Based IPS)

Protects a local machine.

#### NIPS (Network-Based IPS)

Protects an entire network.

---

# Detection Techniques

## Signature-Based Detection

* Uses predefined rules/signatures.
* Fast and accurate for known threats.
* Cannot detect unknown attacks.

## Behavior-Based Detection

Also known as:

* Network Behavior Analysis (NBA)

Requires a training period called:

* Baselining

Advantages:

* Detects unknown attacks.
* Identifies anomalies.

Disadvantages:

* Higher false positives.

---

# Snort Modes

## 1. Sniffer Mode

Reads packets and displays them on the console.

```bash
sudo snort -v
```

Options:

```bash
-v     Verbose output
-d     Display payload
-e     Display link-layer headers
```

Example:

```bash
sudo snort -dev
```

---

## 2. Packet Logger Mode

Logs packets to disk.

```bash
sudo snort -dev -l .
```

Output stored in:

```text
./<IP_ADDRESS>/
```

ASCII logging:

```bash
sudo snort -dev -K ASCII -l .
```

---

## 3. NIDS Mode

Uses configuration files and rules.

```bash
sudo snort -c /etc/snort/snort.conf
```

Common options:

```bash
-c    Configuration file
-A    Alert mode
-l    Log directory
-r    Read pcap file
```

Example:

```bash
sudo snort -c /etc/snort/snort.conf -A full -l .
```

---

# Snort Version Information

Check version:

```bash
snort -V
```

THM Room Values:

```text
Build Number: 149
```

---

# Testing Configuration

Default configuration:

```bash
sudo snort -T -c /etc/snort/snort.conf
```

Loaded rules:

```text
4151
```

Alternative config:

```bash
sudo snort -T -c /etc/snort/snortv2.conf
```

Loaded rules:

```text
1
```

---

# Reading PCAP Files

Read a pcap:

```bash
snort -r file.pcap
```

Read only first 10 packets:

```bash
snort -r file.pcap -n 10
```

Example:

```bash
snort -r snort.log.1640048004 -n 10
```

---

# Useful PCAP Analysis Commands

Read packet capture:

```bash
snort -r snort.log.1640048004
```

Run with configuration:

```bash
sudo snort -c /etc/snort/snort.conf -A full -l . -r file.pcap
```

Read multiple pcaps:

```bash
sudo snort -c /etc/snort/snort.conf -A full -l . \
--pcap-list="mx-2.pcap mx-3.pcap"
```

---

# Snort Rule Structure

Basic syntax:

```bash
action protocol src_ip src_port direction dst_ip dst_port (options)
```

Example:

```bash
alert tcp any any -> any 80 (msg:"HTTP Traffic"; sid:1000001; rev:1;)
```

---

# Rule Components

## Action

```text
alert
log
pass
drop
reject
sdrop
```

---

## Protocol

```text
tcp
udp
icmp
ip
```

---

## Source / Destination

Examples:

```bash
any any -> any 80
```

```bash
192.168.1.0/24 any -> any any
```

---

## Direction Operators

```text
->   One-way
<>   Both directions
```

---

# Common Rule Options

## Message

```bash
msg:"Detected HTTP GET";
```

## Content Match

```bash
content:"GET";
```

## SID

```bash
sid:1000001;
```

## Revision

```bash
rev:1;
```

Important:

After modifying a rule:

```text
Increment rev value.
```

---

# Detecting TCP Flags

## SYN Packet

```bash
flags:S;
```

---

## PUSH + ACK

```bash
flags:PA;
```

---

# Sample Rules

## Detect HTTP GET

```bash
alert tcp any any -> any 80 \
(msg:"HTTP GET"; content:"GET"; sid:1001; rev:1;)
```

---

## Detect Specific IP ID

```bash
alert ip any any -> any any \
(msg:"IP ID Match"; id:35369; sid:1002; rev:1;)
```

---

## Detect SYN Packets

```bash
alert tcp any any -> any any \
(msg:"SYN Packet"; flags:S; sid:1003; rev:1;)
```

---

## Detect Push-Ack Packets

```bash
alert tcp any any -> any any \
(msg:"PUSH ACK"; flags:PA; sid:1004; rev:1;)
```

---

## Detect Same Source and Destination IP

```bash
alert ip any any -> any any \
(msg:"Same Src/Dst"; sameip; sid:1005; rev:1;)
```

---

# Important Room Findings

## Traffic Generator Exercise

Source port connecting to DNS (53):

```text
3009
```

---

## snort.log.1640048004

### 10th Packet IP ID

```text
49313
```

### 4th Packet Referer

```text
http://www.ethereal.com/development.html
```

### 8th Packet ACK

```text
0x38AFFFF3
```

### TCP Port 80 Packets

```text
41
```

---

# Alert Investigation Results

## TASK-7

HTTP GET detections:

```text
2
```

---

## mx-1.pcap

Default configuration:

```text
Alerts: 170
TCP Segments Queued: 18
HTTP Response Headers Extracted: 3
```

Using snortv2.conf:

```text
Alerts: 68
```

---

## mx-2.pcap

```text
Alerts: 340
TCP Packets: 82
```

---

## mx-2 + mx-3

```text
Alerts: 1020
```

---

# Rule Writing Exercise Answers

## IP ID 35369

Request name:

```text
TIMESTAMP REQUEST
```

---

## SYN Rule

Detected packets:

```text
1
```

---

## PUSH-ACK Rule

Detected packets:

```text
216
```

---

## Same Source and Destination IP Rule

Detected packets:

```text
10
```

---

# Key Exam Notes

### Host Detection

```text
HIDS
```

### Host Prevention

```text
HIPS
```

### Network Detection

```text
NIDS
```

### Network Prevention

```text
NIPS
```

### Similar to NIPS

```text
NBA
```

### NBA Learning Period

```text
Baselining
```

### Snort Description

```text
Full-blown NIPS
```

### Rule Version Option

```text
rev
```

---

# Quick Command Cheat Sheet

```bash
snort -V
```

Check version

```bash
snort -T -c /etc/snort/snort.conf
```

Test configuration

```bash
snort -dev
```

Sniffer mode

```bash
snort -dev -K ASCII -l .
```

ASCII logging

```bash
snort -r capture.pcap
```

Read pcap

```bash
snort -r capture.pcap -n 10
```

Read first 10 packets

```bash
snort -c /etc/snort/snort.conf -A full -l .
```

NIDS mode

```bash
snort -c local.rules -A full -l . -r capture.pcap
```

Run custom rules against pcap

---

# SOC Analyst Takeaways

* Understand IDS vs IPS.
* Know HIDS/HIPS and NIDS/NIPS differences.
* Be comfortable reading pcap files with Snort.
* Understand Snort rule syntax.
* Practice TCP flag detection.
* Learn content matching and payload inspection.
* Remember SID and REV management.
* Know how to troubleshoot configuration files.
* Be able to investigate alerts generated from pcaps.
