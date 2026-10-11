> There isn't much information involving DNS that is required to function at the LPIC1 level. A broad discussion of the many areas encompassed by DNS is impossible in this format, so we'll concentrate on the basics and some areas you'll see that might be a surprise.

# # Components of DNS

The primary components of DNS include the DNS server daemon, `named`, the `/etc/named.conf` file (for version 2 and above) or `/etc/named.boot` (for version 4), and the zone files that define a zone or domain.

Typically, the Berkeley Internet Name Domain (BIND) package is included when the distribution is installed, or at least when the typical server installation is selected.

The typical configuration includes the following files:

+   - **Zone files**—These are typically named with a zone name and `.db`, such as `example.db`, and map the hostname to an IP.

+   - **Reverse zone files**—These are named oddly, with a reversed network address followed by `.in-addr.arpa`. So the name for the `192.168.33.0` network would be `0.33.168.192.in-addr.arpa` and contain a reverse mapping of the IP to the hostname.

+   - **named configuration files**—The `/etc/named.conf` or `/etc/named.boot` files depending on the version; these contain the parameters for the DNS daemon and point to the correct zone and hints files.

+   - **Hints files**—These files contain the root server information, which is referred to if the server can't find a resolution through its data or configured servers.

# # Types of DNS Servers

DNS servers come in three main types and functions:

+   - **Master**—The authority for a domain or zone, it contains the physical files that define that domain.

+   - **Slave**—Used to provide load balancing and name resolution for far-flung networks or hosts, it receives zones only from the master.

+   - **Cache**—Used to cache resolved requests for a longer time than other servers, it can query only other configured servers. It has no zone or domain files itself.