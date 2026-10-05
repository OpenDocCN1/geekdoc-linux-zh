# 1.4.5. Caching Name Servers

The resolver libraries provided by most operating systems are stub resolvers, meaning that they are not capable of performing the full DNS resolution process by themselves by calling directly to the authoritative servers. Instead, they rely on a local name server to perform the resolution on their behalf. Such a server is called a recursive name server; it performs recursive lookups for local clients.

To improve performance, recursive servers cache the results of the lookups they perform. Since the processes of recursion and caching are intimately connected, the term recursive server and caching server are often used synonymously.

The length of time for which a record may be retained in the cache of a caching name server is controlled by the Time To Live (TTL) field associated with each resource.

# 1.4.5.1. Forwarding

Even a name server does not necessarily perform the recursive lookup itself. Instead, it can forward some or all of the queries that it cannot satisfy from its cache to another name server, commonly referred to as a forwarder.

There may be one or more forwards, and they are queried in turn until the list is exhausted or an answer is found. Forwards are typically used when you do not wish all the servers at a site to interact directly with the Internet servers. A typical scenario would involve a number of internal DNS servers and an Internet firewall. Servers unable to pass packets through the firewall forward to the server that can do it, and that server query the Internet DNS servers on the internal server's behalf. An added benefit of using the forwarding feature is that the central machine develops a much more complete cache of information that all the clients can take advantage of.

# 1.4.6. Name Servers in Multiple Roles

The BIND name server can simultaneously act as a master for some zones, a slave for other zones, and as a caching (recursive) server for a set of local clients.

However, since the functions of authoritative name service and caching/recursive name service are logically separate, it is often advantageous to run them on separate servers. A server that only provides authoritative name service (an authoritative-only server) can run with recursion disabled, improving reliability and security. A server that is not authoritative for any zones and provides recursive service to local clients (a caching-only server) does not need to be reachable from the Internet at large and can be placed inside a firewall.