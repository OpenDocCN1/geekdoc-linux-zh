# BIND

The DNS server software currently in use on Linux systems is Berkeley Internet Name Domain (BIND). BIND was originally developed at the University of California, Berkeley, and is currently maintained and supported by the Internet Software Consortium (ISC). You can obtain BIND information and current software releases from its Web site at www.isc.org. Web page documentation and manuals are included with the software package. RPM packages are available at distribution FTP sites. The BIND directory in /usr/share/doc contains extensive documentation, including Web page manuals and examples. The Linux HOW-TO for the Domain Name Service, DNS-HOWTO, provides detailed examples. Documentation, news, and DNS tools can be obtained from the DNS Resource Directory (DNSRD) at www.dns.net/dnsrd. The site includes extensive links and online documentation, including the BIND Operations Guide (BOG). See Table 34-2 for a list of DNS resources.

# Alternative DNS Servers

Several alternative DNS servers are now available. These include djbdns, noted for its security features, CustomDNS, a dynamic server implemented in Java (customdns.sourceforge.net), and Yaku-NS, an embedded server. The djbdns server (cr.yp.to/djbdns.html), written by D.J. Bernstein, is designed specifically with security in mind, providing a set of small server daemons, each performing specialized tasks. In particular, djbdns separates the name server, caching server, and zone transfer tasks into separate programs: tinydns (tinydns.org) implements the authoritative name server for a network, whereas dns cache implements a caching server that will resolve requests from DNS clients such as Web browsers. In effect, dns cache operates as the name server that your applications will use to resolve addresses. dns cache will then query tinydns to resolve addresses on your local network. Zone transfers are handled separately by axfrdns and asfet.

**Table 34-2: BIND Resources**

| Web Site | Resource |
|---|---|
| www.isc.org | Internet Software Consortium |
| www.dns.net/dnsrd | DNS Resource Directory |
| www.nominum.com | Nominum, BIND support and consulting |

# DNS Documentation

Currently, ISC has contracted with two companies, Nominum and Mind, to provide BIND support. Nominum is an ISC support partner and has taken an active role in BIND development. At its Web site at www.nominum.com, you can find BIND documentation, including the BIND 9 Administrator's Reference. Nominum, like many commercial companies that support open source software, provides professional consultant and support services, while freely contributing to Open Source development. Mind provides consulting services for the European market.

# BIND Servers and Tools

The BIND DNS server software consists of a name server daemon, several sample configuration files, and resolver libraries. As of 1998, a new version of BIND, beginning with the series number 8.x, implemented a new configuration file using a new syntax. Version 9.0 adds new security features and support for IPv6. Older versions, which begin with the number 4.x, use a different configuration file with an older syntax. Most distributions currently install the newer 9.x version of BIND.

The name of the BIND name server daemon is named. To operate your machine as a name server, simply run the named daemon with the appropriate configuration. The named daemon listens for resolution requests and provides the correct IP address for the requested hostname. You can use the Remote Name Daemon Controller utility, rndc, provided with BIND to start, stop, restart, and check the status of the server as you test its configuration. rndc with the stop command stops named and, with the start command,