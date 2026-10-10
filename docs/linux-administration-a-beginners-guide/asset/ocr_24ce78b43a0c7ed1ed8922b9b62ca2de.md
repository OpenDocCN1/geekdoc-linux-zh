| Tools Installed with BIND Compile/Installation | Description |
|---|---|
| /usr/bin/dig | Shows the process of queries by which an address gets resolved, including all the intermediate DNS servers involved. |
| /usr/bin/dnsquery | Another alternative to nslookup |
| /usr/bin/host | Another alternative to nslookup |
| /usr/sbin/named | The actual server process responsible for providing DNS services. |
| /usr/sbin/named-xfer | An auxiliary program executed by named to get information from other DNS servers. This provides a more powerful tool set for debugging zone transfers, a mechanism by which one DNS server receives data about all the hosts in another DNS server’s tables. (More about this later in the chapter.) |
| /usr/sbin/ndc | A program for controlling the named program. |
| /usr/bin/nsupdate | Allows you to update information in the DNS table in a live server. |
| /usr/sbin/named-bootconf | A utility for converting BIND version 4 configuration files to BIND version 8. |

> Table 12-1.  Files Installed by a BIND Compile/Install (continued)

# CONFIGURING CLIENTS

In this section and the next, we’ll delve into the wild and exciting process of configuring DNS clients and servers! Okay, so maybe they’re not that exciting— but they’re no denying their significance to the infrastructure of any networked site. So you’d best be able to get a few warm and fuzzy feelings about DNS configurations.

# Client-Side DNS (a.k.a. the Resolver)

So far we’ve been studying servers and the DNS tree as a whole. The other part of this equation is, of course, the client—the host that’s contacting the DNS server to resolve a host name into an IP address.