• *Resolvers*. Client programs generate requests for DNS information and send them to name servers for fulfillment. A resolver has direct access to at least one name server and can also process referrals to direct its queries to other name servers when necessary.

In its most basic form, the DNS name resolution process consists of a resolver submitting a name resolution request to its designated DNS server. If the server does not possess authoritative information about the requested name, it can forward the request to another DNS server on the network if configured to do so. Network administrators can choose whether their DNS servers participate in forwarding requests. The second server generates a response containing the IP address of the requested name and returns it to the first server. The first server relays the information to the resolver. In practice, however, the DNS name resolution process can be considerably more complex.

For DNS to function, the namespace must be divided in a way that distributes it among many servers. Also, servers must be able to locate the authoritative source for a particular name. To accomplish these goals, the developers of the DNS created the concept of the *DNS domain*. A domain is an administrative entity that consists of a group of hosts, usually a combination of computers, routers, printers, and other TCP/IP–enabled devices. The DNS namespace consists of a hierarchy of domains, and each domain has DNS name servers that are responsible for supplying information about the hosts in that domain, as shown in Figure 12-1. The designated name servers for a particular domain are the authoritative source of information about that domain. When a DNS server is the authoritative source for a domain, it possesses information about the hosts in that domain, which it stores in the form of resource records.

# Figure 12-1
Hierarchy of domains

![](bbox=[0.23, 0.49, 0.63, 0.79])

WARNING  In the context of DNS, the term *domain* has a different meaning than it has in Active Directory. In Active Directory, a Windows Server 2008 domain is a grouping of Windows computers and devices that are administered as a unit. In DNS, a domain is a group of hosts, and possibly sub-domains, that represent a part of the DNS namespace.

To fully understand DNS, you should be aware of the following configuration items:

• *Resource record*. The resource record is the fundamental data storage unit in all DNS servers. When DNS clients and servers exchange name and address information, they do so in the form of resource records. The most basic common resource record is the Host (A) resource record, which consists of the host name and its IP address. However, DNS servers can also store other types of resource records, some of which are described in the following sections. This record is the logical entry which represents a physical TCP/IP–enabled device on the network.