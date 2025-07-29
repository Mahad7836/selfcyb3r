 Email Fundamentals & Analysis

1. What Makes Up an Email Address?

An email address consists of:

Username: Identifies the recipient (e.g., john.doe)
@ Symbol: Separator between local and domain parts
Domain Name: Mail server address (e.g., example.com)
Full example: john.doe@example.com

2. How an Email Travels (Email Flow):

Step-by-step journey:

User sends email using an email client (MUA – Mail User Agent)
Email is sent to the sender’s SMTP server
SMTP server routes the email via the internet
Recipient’s mail server (via MX records) receives the email
Recipient accesses it via their MUA (using POP3/IMAP)

3. Viewing Email Header Source Code:
Purpose: Reveals routing path, sender info, timestamps, IP addresses

How to view:

Gmail: “Show original”
Outlook: “View message source”
Thunderbird: “View > Headers > All”

Key header fields:

From, To, Subject
Received (shows servers passed through)
Return-Path, Message-ID, Reply-To

4. Viewing Email Body Source Code:
Purpose: Examine content, detect hidden links or malicious scripts

How to view:
Use “View Source” or “Inspect” options in email clients

May contain:
Plain text & HTML
Inline scripts, links, image references (often used for tracking)

5. Important Info to Extract When Analyzing Emails:
Sender address (check for spoofing)
Email subject and content
Header fields (Return-Path, Received lines)
Links (hover to check destinations)
Attachments (file types, suspicious names)
Anomalies in grammar, urgency, tone

6. Common Attacker Techniques in Spam/Phishing:

Spoofed sender addresses
Lookalike domains (e.g., micros0ft.com)
Urgent language to trigger panic or immediate action
Malicious links or attachments (e.g., .exe, .scr, fake PDFs)
Embedded images instead of text (evades filters)
Hidden URLs behind text like “Click here”