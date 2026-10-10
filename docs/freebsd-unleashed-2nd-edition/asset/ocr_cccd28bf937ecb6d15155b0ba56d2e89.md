clients to get immediate responses to their DNS queries from the local server without the queries having to travel out over the Internet. However, this means that changes to DNS records at the authoritative DNS will not be available to the client until the expiration period has passed. Until that time, the DNS information the client sees is “stale” and potentially inaccurate. The time period between DNS cache updates can be controlled for each domain using the Time-To-Live (TTL) value, which you will learn more about later in this chapter.

# DNS Software: BIND

DNS software is ubiquitous. For Unix systems, which account for the vast majority of name servers on the Internet, the software of choice is BIND, by the Internet Software Consortium (ISC). BIND, short for Berkley Internet Name Domain, consists of one major daemon program (named), a set of resolver libraries that provides the ability to perform name lookups, and various administrative tools. BIND is built in to FreeBSD, although it is not enabled by default.

# Zones

BIND allows you to define zones, which are logical groupings of IP addresses and hostnames that exist at a certain level in the DNS naming hierarchy. For example, com is a zone under the root (.) zone, and somewhere.com is a zone that exists underneath the com zone. Note that zone names always end in a dot, referring to the root zone—this will be important when you create your zone files! Subdomains are zones managed by the individual domain name servers; cluster.somewhere.com is a zone that can have multiple machines inside it—indeed, it can have as many further subdivisions within it as you are willing to configure. These zones provide forward DNS lookups, or mappings from names to IP addresses.

Similarly, reverse DNS lookups—or mappings from IP addresses to hostnames—are managed in zones. Because DNS and IP addresses have their roots in the ARPANet (see Chapter 21 for details) and have not changed fundamentally in structure since that time, a reverse DNS zone name is of the form C C C.B B B.A A A.in-addr.arpa. This is a name constructed of the IP address space in reverse order, with .in-addr.arpa appended to it. For example, the 64.41.131.* network would be defined by the zone 131.41.64.in-addr.arpa.

Each zone that your name server will manage must be defined in a zone file—a formatted set of definitions that maps hostnames to IP addresses (or vice versa) within the zone. A zone file also contains parameters for the behavior of the zone, such as the caching expiration period. The zone files are the most critical part of proper DNS configuration; we will be discussing them in detail later in this chapter.

# BIND Files and Programs

Because BIND is a built-in part of FreeBSD, you don’t need to worry about installing it or making sure the proper files are in the proper places. It is worthwhile, though, to know

![](bbox=[0.92, 0.14, 0.98, 0.18])