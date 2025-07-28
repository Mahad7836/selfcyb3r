DNS – How Domain Names Actually Work 


How does your computer turn something like www.google.com into an IP address it can understand?
The answer lies in something called DNS (Domain Name System) – part of the TCP/IP protocol suite.

When you type a URL into your browser, your computer needs to find the IP address that matches that domain name. It does this by asking a DNS server – a special server that knows how to look up this info.

example:

You go to www.google.com.

Your computer sends a request to a DNS server it already knows about.

That DNS server looks up Google’s IP and sends it back.

Now your computer can talk directly to Google’s server.

Let’s Break It Down Step by Step:

First, your computer checks a local file called the Hosts File.

This is old-school.
It manually maps domain names to IPs.
Rarely used today, but still checked first just in case.

If the Hosts File doesn’t have anything, your computer checks its local DNS cache.
If it already looked up this site recently, it might have the IP stored.
If it finds it here – great, no need to go further.

If it’s not cached, your computer sends the request to a recursive DNS server.

These are usually provided by your ISP, Google (8.8.8.8), or OpenDNS.

Your router or OS already knows where to find these.

The recursive DNS server also has a cache – but if it doesn’t know the answer, it moves up the chain...

If the recursive server doesn’t have the info, it asks a Root Name Server.

These servers know where to find the servers responsible for Top-Level Domains (TLDs) like .com, .net, .org, etc.

Next, the root server points the recursive server to a TLD server, depending on the domain.

example:

tryhackme.com → goes to a .com TLD server
bbc.co.uk → goes to a .co.uk TLD server

These servers handle specific domain extensions and know where to find the final answer.

The TLD server sends the request to an Authoritative Name Server.

This server holds the actual DNS records for the domain.

Think of it as the official source of truth for that domain’s IP address.

Finally, the authoritative server sends back the IP address to the recursive server → your computer → your browser.
----------------------------------------------------------------------------------------------------------------------------------
Bonus: Manual Lookup with dig
This whole DNS lookup process happens automatically in the background – super fast. But if you want to do it manually, you can use a command-line tool called dig.
It lets you directly query DNS servers to see how a domain resolves.
Great for troubleshooting or learning how DNS really works.
It’s usually pre-installed on Linux systems.