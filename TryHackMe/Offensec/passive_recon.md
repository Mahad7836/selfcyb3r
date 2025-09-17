# Passive Reconnaissance - THM ROOM

## What is Passive Reconnaissance?

Passive Reconnaissance involves gathering information about a target system, network, or organization without directly interacting with the target. This method avoids detection and leaves no trace on the target's systems.

### Key Aspects of Passive Reconnaissance:

No Direct Interaction:
The attacker doesn't touch or interact with the target system directly.
Focuses on publicly available data.

Collecting Open-Source Intelligence (OSINT):
OSINT is the primary method of passive reconnaissance. It involves gathering information from publicly accessible resources like:

-WHOIS databases
-Social media platforms (LinkedIn, Facebook, Twitter)
-Domain Name System (DNS) records
-Public code repositories (GitHub, GitLab)
-Web archives (Wayback Machine)
-Search engines

Identifying and Mapping Target Information:
Domain names and IP addresses associated with the target.
Subdomains and their structure (potential attack surface).
DNS records for details about mail servers, nameservers, etc.
Technologies used by analyzing website headers or technologies (e.g., Wappalyzer, BuiltWith).
Email addresses, phone numbers, and physical addresses found online.

### Tools for Passive Reconnaissance:

WHOIS Lookup tools (e.g., whois.domaintools.com) for domain information.
DNS Lookup tools (e.g., dnsdumpster.com) to identify DNS records.
Shodan for identifying exposed devices or services.
TheHarvester for gathering emails, domains, and other details.
Google Dorking for advanced search queries.
Maltego for mapping relationships between entities (emails, domains, people).
Wayback Machine for historical data of websites.
Recon-ng is an integrated web reconnaissance framework.

Analyzing Social Media and People Information:
Collecting information about employees or individuals working at the target organization, including job roles, technologies they might use, and organizational structure.
LinkedIn is often a goldmine for employee roles, technologies used, and possible insights into security gaps.

Examining Network Infrastructure:
Passive DNS tools to examine historical and current DNS records.
Identify IP ranges and subnets associated with the organization.
Analyze SSL certificates for information about the hosting provider or infrastructure.

Reviewing Public Documents and Leaked Data:
Searching for exposed information in public data breaches or leaks on platforms like Have I Been Pwned, Pastebin, or Dehashed.
Examining PDFs, Word documents, or other publicly available files that may contain metadata or embedded sensitive information.

## Why Passive Reconnaissance is Critical:

Stealthy: No direct interaction with the target minimizes the risk of detection.
Comprehensive: Provides a wealth of information without the need to engage directly with systems.
Lays the Groundwork: Helps identify attack vectors, weak points, and useful information for further attacks (e.g., phishing, social engineering).

## Challenges in Passive Reconnaissance:

Data Overload: Gathering massive amounts of data can overwhelm the attacker. Identifying actionable intelligence from large datasets requires expertise.
Outdated Information: Public data may be outdated or inaccurate, leading to false conclusions.
Public Records Limitations: Publicly available data may be limited, requiring advanced techniques to gather more detailed information.

## Ethical Considerations:

Passive reconnaissance is typically legal as long as it's conducted using publicly available information.

However, be mindful of local laws and regulations regarding data collection and privacy.

Example Workflow:

Start with a Domain: Gather information using WHOIS and DNS tools.
Social Media Scraping: Search platforms like LinkedIn for employee details and technologies used.
IP and Subdomain Discovery: Use tools like Shodan and Sublist3r to identify other active systems related to the domain.
Public Code Repositories: Search for publicly available code on GitHub or GitLab for any exposed credentials.
Search Engines: Use Google Dorking techniques to find hidden information or data leaks.
Check Historical Information: Explore the Wayback Machine to get old versions of the target’s website and services.