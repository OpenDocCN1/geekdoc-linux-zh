Each of the resource records belonging to a domain store same a different type of information.
For example,

+   - (Address) records store the IP address associated with a name.
- NS (Name Server) records name an authoritative name server for a domain.
- SOA (Start of Authority) records contain basic properties of the domain and the domain's zone.
- PTR (Pointer) records contain the real name of the host to which the IP belongs.
- MX (Mail Exchanger) records specify a mail server for the zone.

Each record type is discussed in detail later in this chapter.

Every node has a unique name that specifies its position in the tree, just as every file has a unique path that leads from the root directory to that. That is, in the domain name, starts with the root domain "*". and prepends to each name in the path, using a dot to separate the names. The root domain has children name com., org., net., de., and so on. They, in turn, have children named ibm.com., wiw.org., and gmx.de.

In general, a fully qualified domain name (FQDN) is one that contains the machine name and the domain name, such as

foo.example.com.

is similar to the following path:

/com/example/foo

Contrary to example, the trailing dot in an FQDN is often omitted. This reverse order is the source of confusion to many people who first examine DNS.

# How Name Servers Store DNS Structure Information

Information about the structure of the tree, and the associated records, is stored by programs called name servers. Every domain has an authoritative name server that holds a complete local copy of the data for the domain; the domain's administrators are responsible for maintaining the data. A name server can also cache information about parts of the tree for which the server has no authority. For administrative convenience, name servers can delegate authority over certain subdomains to other, independently maintained, name servers.

The authoritative name server for a zone knows about the name servers to which over subdomains has been delegated. It might refer queries about the delegated zones