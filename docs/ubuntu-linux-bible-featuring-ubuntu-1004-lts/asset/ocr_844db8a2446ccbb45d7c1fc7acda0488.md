# Chapter 32: Setting Up a DNS Server

forwarding is greatly invisible to you and most often occurs when querying hosts on subdomains rather than top-level domains.

This combination of local, root, and hierarchical name servers is elegant in its simplicity. When your host finally receives the hostname or IP address that it is looking for, it typically caches value so that subsequent requests for the same information won't have to go any further than the local name server.

BIND is generally configured in one of four ways:

+   * As a master server that is an authoritative source of DNS information for one or more zones, which generally map to a domain or subdomain
* As a slave server that is an authoritative source of DNS information for one or more zones, and periodically retrieves and synchronizes this information from a master server rather than being the actual repository for that information
* As a caching-only server that is not authoritative for any zone, but that caches the results from DNS queries to minimize network traffic and expedite multiple requests for the same DNS information. Most Ubuntu Server systems will run at least a caching-only name server for these reasons.
* As a resolver-only client that does not run a DNS server but whose DNS resolver is configured to consult name servers through its /etc/resolv.conf file

Most desktop systems do not need to actually run a name server and will work fine as resolver-only clients. However, if you spend a vast amount of time surfing the Web or on a heavily loaded network, you might want to upgrade your system to running a caching-only client. DNS servers do not consume a vast amount of system resources, but they do require memory, process slots, and so on. If you have a few machines. If a system that you are configuring or using does not need to provide host information for a zone (which would mandate running a DNS server), only the user(s) of a system can determine which of the caching-only or resolver-only configurations works best for that.

# Installing a DNS Server

Although every Ubuntu system provides the basic client-side commands for querying and dynamically mapping hostnames to IP addresses, an actual DNS server is not installed as part of a default Ubuntu installation. Lets face it—not everybody needs to run a DNS server, and for small, home networks, maintaining your /etc/hosts files isn't that of an issue if you only have a few machines. However, if you want to run your own name server (which probably want to do if you are responsible for an enterprise network or SHO network with a relatively large number of hosts), the package management utilities provided on Ubuntu systems make it easy to install the BIND DNS server by installing the bind9 package. See Chapter 19, "Adding, Removing, and Updating Software," for more information about installing software on Ubuntu systems.