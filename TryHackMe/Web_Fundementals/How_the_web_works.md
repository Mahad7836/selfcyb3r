
Load Balancers provide 2 main features, ensuring high traffic websites can handle the load and providing a failover if a server becomes unresponsive

If you request a website with a load balancer, the LB receives the request first then checks which server is best to deal with
They also to periodic checks to ensure each server is running correctly aka Health Check

CDN- Content Delivery Network, allows you to host static files from your website and host them across thousands of servers all over the world

WAF- web app. firewall

web server listens for incoming connections and then utilizes HTTP protocol 
it delivers files from its root directory

web servers can host different domain names, to achieve this they use virtual hosts

static content e.g javascript,css
dynamic content e.g a blog

Request tryhackme.com in your browser -> check local cache for IP address -> check your recursive DNS Server for address -> query root server to find authoritative DNS Server -> authoritative DNS Server advises IP address for the website -> Request passes through WAF -> Request passes through LB -> Connect to webserver on port 80/443 -> Web server receives GET request -> Web App. talks to DB -> browser renders HTML
