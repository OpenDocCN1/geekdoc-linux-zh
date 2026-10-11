![](bbox=[0.05, 0.2, 0.45, 0.62])

First, a computer requests a resolution for a FQDN — for example, **server12.prod.transcont.net**. The client sends the request to a local DNS server for resolution. If the DNS server does not have authority over the domain **corp.com**, then it has to go through a resolution process with other servers, beginning with an Internet root server. The DNS server asks the Internet root server for the IP address of a “com” server to begin the resolution process.

![](bbox=[0.5, 0.42, 0.95, 0.73])

# Understanding name resolution

Fully Qualified Domain Names (FQDN) must be resolved to IP addresses in order for network communication to occur. The DNS name resolution process is performed by resolving each domain in FQDN, beginning at the top of the hierarchy and working its way down. On your network, a DNS server may be able to check its database file and resolve a FQDN to an IP address. On the Internet, this process normally requires several servers. Different DNS servers must resolve each portion of the DNS name until the host is eventually reached and an IP address can be returned. This process is called a *forward lookup query*.

The Internet root returns the IP address of a com server, and then the DNS server contacts this server for the IP address of a “corp” DNS server. The com server checks its database and returns the IP address of a transcont DNS server.