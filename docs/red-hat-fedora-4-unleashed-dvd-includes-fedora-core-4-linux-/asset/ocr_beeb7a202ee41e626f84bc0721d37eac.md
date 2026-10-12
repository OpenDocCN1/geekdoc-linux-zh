is similar to the following path:

```
/com/example/foo
```

Contrary to the example, the trailing dot in an FQDN is often omitted. This reverse order is the source of confusion to many people who first examine DNS.

# ## How Nameservers Store DNS Structure Information

Information about the structure of the tree, and its associated resource records, is stored by programs called nameservers. Every domain has an authoritative nameserver that holds a complete local copy of the data for the domain; the domain's administrators are responsible for maintaining the data. A nameserver can also cache information about parts of the tree for which the server has no authority. For administrative convenience, nameservers can delegate authority over certain subdomains to other, independently maintained, nameservers.

The authoritative nameserver for a zone knows about the nameserver to which authority over subdomains has been delegated. The authoritative nameserver might refer queries about the delegated zones to those nameservers. So, we can always find authoritative data for a domain by following the chain of delegations of authority from . (the root domain) until we reach an authoritative nameserver for the domain. This is what gives DNS its distributed tree structure.

# ## How DNS Provides Name Service Information to Users

Users of DNS need not be aware of these details. To them, the namespace is just a single tree—any part of which they can request information about. The task of finding the requested RRs from the resource set for a domain is left to programs called resolvers. Resolvers are aware of the distributed structure of the database. They know how to contact the root nameservers (which are authoritative for the root domain) and how to follow the chain of delegations until they find an authoritative nameserver that can give them the information they are looking for.

At the risk of stretching the analogy too far, you can think of domains as directories in a file system and resource records as files in these directories. The delegation of authority over subdomains is similar to having an NFS file system mounted under a subdirectory: Requests for files under that directory would go to the NFS server, rather than this file system. The resolver's job is to start from the root directory and walk down the directory tree (following mount points) until it reaches the directory that contains the files they are interested in. For efficiency, they can then cache the information they find for some time. This is why things appear to be listed in “reverse” order. This process is examined in detail next.

In practice, there are several authoritative nameservers for a domain. One of them is the master (or primary) nameserver, where the domain's data is held. The others are known as slave (or secondary) nameservers, and they hold automatically updated copies of the master data. Both the master and the slaves serve the same information, so it doesn't