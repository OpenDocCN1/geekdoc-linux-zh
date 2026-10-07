# NOTE

Retaining and frequently examining your logs is especially important because syntax errors often cause BIND to reject a zone and not answer queries for it, causing your server to become lame (that is, not authoritative for a zone for which it is supposed to be).

# Resolver Configuration

The last step before running BIND is to set up the local resolver software. This involves configuring the /etc/hosts, /etc/resolv.conf, and /etc/nsswitch.conf files.

To avoid gratuit network traffic, most Unix resolvers use a hosts.txt-like file named /etc/hosts to store the names and addresses of commonly used hosts. Each line in this file contains an IP address and a list of names for the host. Add entries to this file for any hosts you want to be able to resolve independently from DNS. If the entry is found in /etc/hosts, the resolver does not have to contact a DNS server to resolve the name, which reduces network traffic.

/etc/resolv.conf specifies the addresses of preferred name servers and a list of domains relative to which unqualified names will be resolved. You specify a name server with a line of the form nameserver1.2.3.4 (where 1.2.3.4 is the address of the name server). You can use multiple nameserver (usually up to three). You can use a search line to specify a list of domains for unqualified names.

A search line such as example.com example.net would cause the resolver to attempt to resolve the unqualified name xyz, first xyz.example.com, and if that fails, as xyz.example.net. Don't use too many domains in the search list because it slows down resolution.

A hosts: dns line in /etc/nsswitch.conf will cause the resolver to consult /etc/hosts before using the DNS during the course of a name lookup. This allows you to override the DNS by making temporary changes to /etc/hosts, which is especially useful during network testing. (Older resolvers might require an order hosts, bind line in the /etc/host.conf instance).

# Running the named Daemon Daemon

Finally! You can now start named with /etc/rc.d/named start. You should see messages similar to the ones that follow in the syslog (or according to the logging configuration you have set up). One way to do this is to monitor the log file with the tail command, that will scroll the changes in the file down the screen.

```
# tail -f /var/log/messages
```

May 9 23:48:33 shuttle named[2605]: starting BIND 9.2.0 -u named
May 9 23:48:33 shuttle named[2605]: using 1 CPU