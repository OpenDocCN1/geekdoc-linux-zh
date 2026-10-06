# Installation

Red Hat Linux includes these BIND-related packages:

+   - bind, which provides a regular DNS server

+   - bind-utils, a set of useful utilities for administering BIND

+   - caching-nameserver, which configures BIND to provide a caching-only name server

In addition, it includes the bind-devel package, which is needed only when doing software development of programs that invoke the BIND application programming interface.

To install BIND, move to the directory that contains the packages and issue the following command

```
rpm -Uvh bind-*.rpm
```

If you want to configure a caching-only name server, also issue the following command

```
rpm -Uvh caching-nameserver-*.rpm
```

# Basic BIND Configuration

To establish Domain Name Service (DNS), you must configure the main DNS configuration file, /etc/named.conf. Generally, you must also configure a set of files known as zone files, which generally reside in /var/named. A zone file is either:

+   - A forward zone file, used to map host names to IP addresses

+   - A reverse zone file, used to map IP addresses to host names

+   - A hint file, which identifies the root name servers responsible for answering DNS queries for all registered domains