
## TABLE 9.5: PROPOSED DOMAINS

| Domain | Description |
| :--- | :--- |
| .aero | Air-transport businesses |
| .arts | Cultural or art organizations |
| .biz | Businesses |
| .coop | Cooperatives |
| .firm | Incorporated businesses, trades |
| .info | Unrestricted |
| .museums | Museums |
| .name, .nom | Personal or individual |
| .pro | Accountants, lawyers, physicians |
| .rec | Recreational, entertainment |
| .store | Online retailers |

As with subdirectories, subdomains are created to associate hosts that are related by physical location or business function. This helps to give organization and order to the hierarchical structure. Subdomains can be created at any time without notification to the top-level domains. Just as in the Solaris parent and child relationship, when the parent top-level domain creates its child, the subdomain, it delegates authority for that subdomain to the child’s name server. Although the parent knows the address of the child’s name server, it doesn’t know about any of the systems located in the subdomain. Subdomains are often referred to as zones. A zone is a piece of the naming tree that is under the administrative control of a particular name server.

Each domain within the DNS tree has a fully qualified domain name (FQDN). This is similar to a path name for a directory in the Unix directory tree. If you want to identify the FQDN, you start by getting the name of the current domain, adding the name of the parent domain, adding the name of the grandparent’s domain, and so on until you reach the root of the tree.

> **TIP** Flexibility in naming is built in to DNS, but to keep the system hearty and scalable, a few conventions are observed. Domain and hosts names must contain only lowercase letters, and uppercase letters will automatically be converted to lowercase. The hyphen character and numerals are allowed. The maximum number of characters in a domain or host name is 63. The maximum number of characters in an FQDN is 255. The maximum number of subdomains is 127. The restrictions are specifically designed to limit the DNS tree to 5 or 6 levels to keep name lookups as fast as possible.

The DNS is based on a query-and-response process. This process is called *name resolution* because it resolves the name of a system right down to its IP address. If a DNS client wants to determine the IP address for a host, it will send a resolution request to its DNS server. That name server will then communicate with other name servers to find the information requested by the client. No single name server knows all of the information about a domain; it knows only what it needs to know at the time. When a name server does not know the address of a host, it just refers the resolver to the name servers listed in the `resolv.conf` file for a different name server that might be able to determine the address. All queries and responses are transmitted using UDP datagrams. These transmission requests are both sent and received by the DNS server on port 53.

Solaris systems by default are not configured to use DNS. However, you can enable the stub resolver to use DNS by modifying the network services configuration file, `/etc/nsswitch.conf`. To enable the DNS, edit the line

```
hosts:      files
```

to read

```
hosts:     files dns
```

You also need to configure the `/etc/resolv.conf` file, which would look like this:

```
$ cat /etc/resolv.conf
domain <domain name>

nameserver <primary name server for system>
nameserver <secondary name server for system>

$
```

You can have many name server listings, one for each system you want to use as a name server. Usually, you have only two or three.

You can configure your system to act as one of three different types of name servers if you so desire. However, most systems should just be clients or they would become overloaded with requests because no system would be caching for any others. If you do choose to configure name servers, number one is the master (or primary) name server and is the most authoritative of the three. It will have the most up-to-date records for all the hosts in its zone. In DNS, the master server is always considered to be absolutely correct. That is why the term *authoritative* is used. Number two is the slave server, which receives its updates from the master name server. It is a replica of the master name server and depends on the master to receive the zone data. The slave lists masters that it can contact to update its copy of the zone. Number three is a hint (or caching) name server and contains just a list of root name servers to resolve queries that it receives. It is not authoritative for any domain.

When a query is made to a hint server for the first time, the hint server forwards the query to an authoritative server. The hint server will then respond to further queries for that host using the IP address in its cache until the entry expires. If you are connecting to an existing network, there may be a name server already configured for it. If you are setting up a new department or a new group within an existing department, you will need to set up at least a hint name server to reduce the load on your master name server. If you are setting up a new site or a new subdomain within an existing site, you must configure a master and perhaps a slave name server.

> **TIP** It is possible to configure a single name server to be master for one domain and slave for another and also act as a hint name server. DNS allows a single name server to have multiple roles.

A master name server responds to queries with authoritative answers for the zone in which it is located. The database file it draws on is called the zone database file, and it contains the host names and corresponding IP addresses for the hosts within the server's zone. The information in the zone database file is stored in the form of resource records. These records store the host name and IP address information in the database along with various other attributes. The master name server can query other name servers and maintain a cache of their responses, which reduces the time needed to resolve frequently accessed host names. It can also delegate the responsibility for subdomains to other name servers. Before the information for a domain controlled by a master name server can be changed, the zone database file must be changed. This file contains an incremental serial number that changes each time the database is altered in order to ensure that slave name servers will obtain the changes.

> **TIP** The most common mistake that DNS administrators make is that they fail to increment the serial number. It is helpful to use a consistent serial numbering scheme, such as, for example, a date notation like 200108021 for 2001, Aug 2, revision 1.

The slave name servers act as backup name servers for the master name server if it crashes or somehow becomes inaccessible. Most domains will have at least one slave name server available. The slave name servers can also query other name servers and store a cache of responses to speed up the response time to frequently accessed host names. The slave name server will synchronize with the database on the master to update the zone information. The synchronization is based on comparing the serial numbers on both databases to make certain they match. If the serial number on the master is larger than that of the slave's, then the slave name server will perform a zone transfer, which is a procedure used by the slave name server for obtaining a new copy of the zone database from the master name server.

The hint servers do not contain authoritative information. Their only purpose is to forward queries to other name servers and cache the answer for a prescribed period of time. When a resolver queries a hint name server, the server will return the answer it has stored in its cache instead of forwarding the query to another name server. Hint name servers are used to reduce DNS traffic within large domains.

To keep your DNS server as secure as possible, you must employ two techniques. The first is to restrict responses, and the second is to restrict zone transfers. Restricting zone transfers to your slave servers is the most important consideration and will offer some security in itself. However, enterprising hackers can always find a way around the zone transfer issue.

Restricting zone transfers that contain all of the information about your zone is the number one priority in keeping your DNS server secure. Your entire zone database could be acquired through an illicit zone transfer. You need to allow queries to your primary or backup domains; otherwise, you won't be able to look up any records for the domains. But you should restrict general queries so others won't use your system as their name server. You need to specify the list of IP addresses that are allowed to initiate zone transfers with your name server. For Solaris 8 (BIND), you will need to specify an allow-transfer parameter for each zone directive in the name server configuration file, /etc/named.conf. The syntax for this parameter is as follows:

```
allow-transfer <address1>; <address2>; <addressN>;
```

In this example, <address1> through <addressN> are either the IP addresses or network addresses from which you want to allow zone transfers. The allow-transfer is a parameter of the zone directive, which means that you need to specify it for every zone directive in order to restrict zone transfers.

The most common Solaris interface to the DNS is the Berkeley Internet Name Domain (BIND) software, which follows the client/server model. On any local network, there may be one or more systems running a name server, supporting all the local hosts as clients. If a system sends a message to another host, it queries the nearest name server to learn the remote host's IP address. The client, or resolver, may be a process running on the same computer as the name server. It may pass the request over the network to reach a server as well. To reduce network traffic and speed up the lookup process, the local name server has some knowledge of distant hosts. When a local server contacts a remote server with a request for an address, after a response, the local server adds that address to its internal table and reuses it for a while. The name server deletes the non-local information before it can become outdated.
