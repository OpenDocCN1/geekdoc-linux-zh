# Authoritative servers

The DNS specifications require at least two authoritative servers for each domain. Master and slave servers are authoritative; caching and stub servers are not. Ideally, a site has multiple authoritative servers, each on a separate network and power circuit. Many sites maintain an authoritative server off-site, often hosted by their ISP. If your ISP does not offer this service, you can purchase it from a DNS service provider or trade with a local firm (ideally, not a competitor) or university.

A few years ago, Microsoft got caught violating the rule of separate networks. They had all three of their authoritative servers on the same subnet, and when the router that connected that subnet to the Internet failed, the servers became unreachable. Two hours later, as cached records expired, microsoft.com and all their other domains dropped off the Internet. The number of queries for Microsoftrelated names at the root servers increased to 25% of the total load (10,000 queries/second), up from their typical value of 0.000001%. Problems persisted for a couple of days. When the dust settled, Microsoft fixed the router and outsourced their DNS service.

Authoritative servers keep their data synchronized using zone transfers. Use TSIG (transaction signature) keys to authenticate and control the zone transfers from your master server to your slave servers. See page 645 for TSIG configuration information.

You may query the responses provided by your authoritative servers to depend on some extent on who is asking. A query from outside your network might receive one answer, while the same query originating inside your organization would receive a different (or more complete) answer. This configuration is called “split DNS” and is implemented at the zone level, not the master server level.

Each version of the zone is called a “view”, after the view statement with which it is configured in the BIND configuration file. External folks see one of the data, and internal folks also. This feature is commonly used to conceal the existence of internal machines from prying eyes and to ensure that machines using RFC1918 private IP addresses do not leak into the Internet. Views are tricky to debug, but BIND’s extensive logging capabilities, together with clever use of the dig command, can help; see page 667 for some hints.

NSD does not support views and split DNS. However, you can simulate this by running two instances of NSD with different configurations. (Of course, you can do that with BIND, too.)

# Caching servers

Recursive caching servers answer local users’ queries about sites on the Internet. Each computer at your site should have ready access to a local caching server.

Some organizations use a hierarchy in which one or more machines are designated as “forwarders” through which the local subnets caching servers pass their