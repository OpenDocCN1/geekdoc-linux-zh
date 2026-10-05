# The BIND software

is also not needed in the glue section since it can be determined by a normal DNS query. An A record in this zone would initially be unnecessary, but it could later become out of date and wrong if ns.cs.colorado.edu’s address were to change. The rule of thumb is to include A records for hosts that are the current domain or any of its subdomains. BIND NSD ignore unnecessary glue records, and BIND logs their presence as an error.

The scheme described is the standard way of connecting zones, but it requires the child to keep in touch with the parent and tell about any changes or additions to its name server fetch. Since parent and child zones are run by different sites, updates can be a tedious manual task that requires coordination across administrative boundaries. A corollary is that in the real world, this type of configuration is out of date.

The second way to maintain links is to use stub zones. A stub zone is essentially the same as a slave zone, but it includes only the NS records and the corresponding A records of name servers. Like a slave, a stub zone is automatically updated and eliminates the need for communication between the administrators of the parent and child zones.

An important caveat is that stub zones must be configured identically on both the master and slave servers of the parent zone. It might be easiest to keep in touch manually with your parent domain and to verify its configuration of times a year (especially if it is local).

You can use the dig command to see of which your servers your parent domain is currently advertising. First run

```
$ dig parent-domain
```

to determine the name servers for your parent domain. Pick one and then run

```
$ dig @name-server.parent-domain child-domain ns
```

to see your list of public name servers. One situation in which stub zones are very useful when your internal network uses RFC1918 private IP address space and you need to keep the RFC1918 delegations in sync.

We have now covered most of the background information that applies to the Domain Name System generally and to its database. In the next section, we cover configuration details specific to the BIND implementation. The NSD/Unbound implementation is covered beginning on page 625.

# 17.9 The BIND software

BIND, the Berkeley Internet Name Domain system, is an open source package from ISC that implements the DNS protocol for Linux, UNIX, Mac OS, and Windows systems. There have been three main flavors of BIND: BIND 4, BIND 8, and BIND 9, with BIND 10 currently under development by ISC. We cover only BIND 9 in this book.