
Each of the resource records belonging to a domain store a different type of information.
For example,

- A (Address) records store the IP address associated with a name.
- NS (Name Server) records name an authoritative name server for a domain.
- SOA (Start of Authority) records contain basic properties of the domain and the domain's zone.
- PTR (Pointer) records contain the real name of the host to which the IP belongs.
- MX (Mail Exchanger) records specify a mail server for the zone.

Each record type is discussed in detail later in this chapter.

Every node has a unique name that specifies its position in the tree, just as every file has a unique path that leads from the root directory to that. That is, in the domain name, starts with the root domain "*." and prepends to each name in the path, using a dot to separate the names. The root domain has children name com., org., net., de., and so on. They, in turn, have children named ibm.com., wiw.org., and gmx.de.

In general, a fully qualified domain name (FQDN) is one that contains the machine name and the domain name, such as

foo.example.com.

is similar to the following path:

/com/example/foo

Contrary to example, the trailing dot in an FQDN is often omitted. This reverse order is the source of confusion to many people who first examine DNS.

## How Name Servers Store DNS Structure Information

Information about the structure of the tree, and the associated records, is stored by programs called name servers. Every domain has an authoritative name server that holds a complete local copy of the data for the domain; the domain's administrators are responsible for maintaining the data. A name server can also cache information about parts of the tree for which the server has no authority. For administrative convenience, name servers can delegate authority over certain subdomains to other, independently maintained, name servers.

The authoritative name server for a zone knows about the name servers to which over subdomains has been delegated. It might refer queries about the delegated zones to those name servers. So, we can always find authoritative data for a domain by following the chain of delegations of authority from "." (the root domain) until we reach an authoritative name server for the domain. This is what gives DNS its distributed tree structure.

## How DNS Provides Name Service Information to Users

Users of DNS need not to be aware of these details. To them, the namespace is just a single tree—any part of which they can request information about. The task of finding the requested RRs from the resource set for a domain is left to programs resolvers. Resolvers are aware of the distributed structure of the database. They know how to contact the root name servers (which are authoritative for the root domain) and how to follow the chain of delegations until they find an authoritative name server that can give them the information they are looking for.

At the risk of stretching the analogy too far, you can think of domains as directories in a filesystem and resource as files in these directories. The delegation of authority over subdomains is similar to having an NFS filesystem mounted under a subdirectory: Requests for files under that directory would go to the NFS server, rather than this filesystem. The resolver's job is to start from the root directory and walk down the directory tree (following mount points) until it reaches the directory that contains the files they are interested in. (For efficiency, they can cache the information they find for some time.) This is why order to be listed in “reverse” order. This process is examined in detail next.

In practice, there are several authoritative name servers for a domain. One of them is the master (or primary) name server, where the domain's data is held. The others are known as slave (or secondary) name servers, and they hold automatically updated copies of the master data. Both the master and the slaves serve the same information, so it doesn't matter which one resolver asks. The distinction between master and slave is made purely for reasons of reliability—to ensure the failure of a single name server doesn't result in the loss of authoritative data for the domain. As a bonus, this redundancy distributes the network load between several hosts so that no name server is overwhelmed with requests for authoritative information.

> As a DNS administrator, it is your responsibility to ensure that your name servers provide sufficient redundancy for your zones. Slave should be far away from the master so that power failures, network outages, and other catastrophes don't affect your name service.

Despite these precautions, the load on DNS servers would be crushing without the use of local caches. As mentioned before, name servers are allowed to cache the results of queries and intermediate referrals for some time so that they can serve repeated requests for data without referring to the source each time. If they didn't do this, root name servers (the name servers for other popular zones) would be contacted by clients all over the world for every name lookup, wasting a huge amount of resources.

## Name Resolution in Practice

When a Web browser issues a request for an IP address, the request is sent to a local server, which resolves the name, stores the result in its cache, and returns the IP address. To better understand this process, take a moment to see what happens behind the scenes when a Web browser issues a request for the IP address of www.ibm.com. This example mimics the actions of the resolver using the incredibly useful dig utility to follow the chain of delegations zones until you find the A record you are looking for. (Because many name servers would follow the delegations for you, this example uses the +norec dig parameter to turn off recursion. That is, if the name server doesn't know how to answer your query, it will not issue further queries about its own.)

> There are 13 name servers around the world. Several are located in the United States (Virginia, California, Maryland). Others are located in London, Tokyo. These root servers do not hold lists of IP addresses, but simply hand off one of the thirteen root servers at random, to ask what it knows about an A record for www.com.

```
$ dig +norec www.com @e.root-servers
;; QUERY: 1
status: NOERROR, status: 0
;; flags: qr, id: 5235
;; SECTION:
www.com.      IN

;; ANSWER SECTION:
;; AUTHORITY SECTION:
a.gtld-servers.net.
b.gtld-servers.net.
c.gtld-servers.net.
d.gtld-servers.net.
e.gtld-servers.net.
f.gtld-servers.net.
g.gtld-servers.net.
h.gtld-servers.net.
i.gtld-servers.net.
j.gtld-servers.net.
k.gtld-servers.net.
l.gtld-servers.net.
m.gtld-servers.net.

;; ADDITIONAL SECTION:
a.gtld-servers.net. 192.56.6.30
b.gtld-servers.net. 192.42.93.30
c.gtld-servers.net. 192.54.112.30
d.gtld-servers.net. 192.26.92.30
e.gtld-servers.net. 192.33.14.30
f.gtld-servers.net. 192.31.80.30
g.gtld-servers.net. 192.41.162.30
h.gtld-servers.net. 210.132.100.101
i.gtld-servers.net. 213.177.194.5
j.gtld-servers.net. 192.12.94.30
k.gtld-servers.net. 202.153.114.101
l.gtld-servers.net. 203.174.133
m.gtld-servers.net. 198.41.0.13
```
;; Query time: 819 msec
;; SERVER: 192.203.230.10#53(root-servers.net)
;; WHEN: Wed Sep 26 10:05:08
;; MSG SIZE rcvd: 461

The ANSWER: 0, in the response means that e.root-servers didn't know the answer to your question. It knows the authoritative servers for the com TLD, and it refers your query to them in the AUTHORITY section. (Not too long ago, the root-servers.net name servers were themselves authoritative for the com TLD, but additional delegations were introduced.)

The resolver's next step would be to select one of these listed servers at random, to use the IP addresses mentioned in the ADDITIONAL section of the response to connect to the server, and repeat the question. This is what we do now, having chosen i.gtld-servers:
