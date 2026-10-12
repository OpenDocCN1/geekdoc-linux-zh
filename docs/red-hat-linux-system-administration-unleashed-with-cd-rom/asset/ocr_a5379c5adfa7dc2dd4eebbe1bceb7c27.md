For systems that run their own name server, the BIND server runs as a distinct process called named (pronounced “name-dee”). Name servers can be divided into three categories, depending on how they are configured.

+   - **Master**—The master server for a domain is the server from which all data about that domain is derived. This data is supplied by the administrator. Master servers are authoritative for their domain. Earlier versions of BIND used the term *primary* instead of master.
+   
+   - **Slave**—Like a master server, a slave server possesses all the information about a domain. The difference is that where a master server gets the data directly from an administrator-supplied file, a slave server gets it from a primary server. Slave servers are also authoritative for their domain. Earlier versions of BIND used the term *secondary* instead of slave.
+   
+   - **Caching-only**—A caching-only server need not hold all the information about any domain and, in fact, it rarely will. It will cache the results of queries, as do most name servers, but it has no other method of building a domain name database. Caching servers are non-authoritative: their information is second-hand and incomplete, though it is usually accurate.

Many servers will combine elements of one or more of these roles. In particular, the BIND documentation actually refers to master and slave zones rather than servers, where a server may serve any number of zones.

# Resolver Library

All UNIX and Linux systems have a resolver library. The resolver has a configuration file, `/etc/resolv.conf`, which allows you to specify which name servers (if any) it will query.

The `/etc/resolv.conf` may contain the following directives:

+   - **nameserver**—There may be up to three nameserver directives, each of which specifies a server to query. The server should be specified as a dotted-quad IP address. Servers after the first are queried if no response is received from earlier ones. If there is no nameserver directive (or if there is no `/etc/resolv.conf` file), the local host is queried. If you specify nameservers explicitly and you want the local host to be queried, you should give its official IP address rather than the loopback address. A resolver-only configuration will never need a nameserver directive that points to the local host.