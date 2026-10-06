
# CHAPTER 16 Domain Name System (DNS) 449

17. Finally you might want to make sure that your DNS server service starts up during the next system reboot. Use the chkconfig command:

```
[root@serverA]# chkconfig named on
```

On a systemd-enabled distro, you can use the following command instead to ensure that named automatically starts up with your system:

```
[root@serverA]# systemctl enable named.service
```

The next section will walk you through the use of tools that can be used to test or query a DNS server.

## The DNS Toolbox

This section describes a few tools that you'll want to get acquainted with as you work with DNS. They'll help you to troubleshoot problems more quickly.

## host

The host tool is a relatively simple utility to use. Its functionality can, of course, be extended by using its various options. Its options and syntax are shown here:

- `host [-acdlrTvw] [-c class] [-n ndots] [-t type] [-W time] [-R number] hostname [server]`
- a is equivalent to -v *
- c specifies query class for non-IN data
- s compares SOA records on authoritative nameservers
- d is equivalent to -v
- l lists all hosts in a domain, using AXFR
- i uses the old IN6.INT form of IPv6 reverse lookup
- N changes the number of allowed dots before root lookup is done
- disables recursive processing
- R specifies number of retries for UDP packets
- t specifies the query type
- enables TCP/IP mode
- v enables verbose output
- w specifies to wait for a reply
- W specifies how long to wait for a reply

In its simplest use, host allows you to resolve hostnames into IP addresses from the command line.

```
[root@serverA]# host internic.net
internic.net has address 192.0.32.9
...<OUTPUT TRUNCATED>...
```

## 450 Linux Administration: A Beginner's Guide

You can also use host to perform reverse lookups. Here’s an example:

```
root@serverA ~# host 198.41.0.6
6.0.41.198-in-addr.arpa domain name pointer rs.internic.net.
```

The host command can also be used to query for IPv6 records. For example, to query (on its ipv6 interface) a name server (::1) for the IPv6 address of the host serverB-v6.example.org, you can run:

```
root@serverA ~# host serverB-v6.example.org ::1
Using domain server:
Name: ::1#53
Address: ::1#53
serverB-v6.example.org has IPv6 address 2001:db8::2
```

To query the PTR record for serverB-v6, you can use the following:

```
root@serverA ~# host 2001:db8::2 ::1
Using domain server:
Name: ::1
Address: ::1#53
Aliases:
2.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.2.ip6.arpa \
domain name pointer serverB-v6.example.org.
```

## dig

The domain information gopher, dig, is a great tool for gathering information about DNS servers. Its syntax and its options are shown here (see the dig page for the meaning of various options):

```
dig [@global-server] [domain] [q-type] [q-class] [q-opt]
{global-d-opt} host [@local-server] {local-d-opt}
[ host [@local-server] {local-d-opt} [...]
```

Where: domain are the dig’s usage summary:

```
dig @server> domain query-type
```

Here, <server> is the name of the DNS server you want to query, domain and query-type is the name of the domain name you are interested in, and the record you are trying to get (A, MX, NS, SOA, HINFO, TXT, ANY, and so on).

For example, to query the MX record for the example.org domain established in the earlier project from the DNS server we set up, you would use the dig command like this:

```
root@serverA ~# dig @localhost example.org MX
```

## CHAPTER 16 Domain Name System (DNS) 451

To query our local DNS server for the A records for the yahoo.com domain, simply type this:

```
[root@serverA ~]# dig @localhost yahoo.com
```

> NOTE: Notice that for the preceding command, we didn't explicitly specify the query type—that is, didn't explicitly specify an A-type record. The default behavior for dig is to assume you want an A record when nothing is specified. You might also notice that we are querying our DNS server for the yahoo.com domain. Our server is obviously not authoritative for the yahoo.com domain, but because we also configured it as a caching-capable DNS server, it is able to obtain the proper answer for us from the appropriate DNS servers.

To query our IPv6-capable DNS server for the AAAA record for the host serverB-v6.example.org, type the following:

```
[root@serverA ~]# dig @localhost serverB-v6.example.org -t AAAA
```

To reissue one of the previous commands, but this time suppress all verbosity using one of dig's options (+short), type this:

```
[root@serverA]# dig +short @localhost yahoo.com
```

To query the local name for the reverse lookup (PTR RR) for 192.168.1.1, type this:

```
[root@serverA]# dig -x 192.168.1.1 @localhost
```

To query the local name for IPv6 reverse lookup (PTR RR) for 2001:db8::2, type this:

```
[root@serverA]# dig -x 2001:db8::2 @localhost
```

The dig program is incredibly powerful. Its options are too numerous to cover properly. Read the man page installed with dig to learn how to use some of its features.

## nslookup

The nslookup utility is one of the tools that you will find across operating systems, so it is probably one of the most familiar tools. Its usage is quite simple, too. It can be used interactively and noninteractively (that is, directly from the command line).

Interactive mode is entered when no arguments are provided to the command. Typing nslookup itself at the command line will drop you to the nslookup shell. To get out of interactive mode, just type exit.

> TIP: When nslookup is used in interactive mode, the command to quit is exit. But most people will often issue the quit command to try the interactive mode. nslookup will think it is being asked to do DNS lookup for the hostname "quit". It will eventually time out. You can create a DNS record that will immediately remind the user of the proper command to use by an entry into this zone file.

The non-interactive mode is summarized here:

```
nslookup [-option] [name] [server]
```

For example, to use nslookup noninteractively to query our local name server for information about www.example.org, you'd type this:

```
root@serverA ~# nslookup www.example.org localhost
```

> NOTE: The developers of BIND frown upon the use of nslookup utility. Even though it is still popular, it has officially deprecated.

## whois

The whois command is used for determining ownership of a domain. Information about a domain's owner isn't a mandatory part of its records, nor is it customarily placed in TXT or SOA records. So you'll need to gather this information using whois technique, which reports the domain owner's actual name, mail-address, e-mail address, and technical contact phone numbers.

Let's try to get information about the example.com domain:

```
root@serverA ~# whois example.com
Querying whois.iana.org... redirected to whois.iana.org
Querying whois.iana.org
whois.iana.org
% IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object
```

domain: EXAMPLE.COM
organisation: Internet Assigned Numbers Authority
created: 1992-01-01
source: IANA

## nsupdate

An forgotten but powerful DNS utility is nsupdate. It is used to submit Dynamic DNS (DDNS) Update requests to a DNS server. It allows the resource records (RR) to be added or removed from a zone without needing to edit the zone database files manually. This is especially useful because DDNS-type zones should not be edited or updated by hand, since the manual changes are bound to conflict with the dynamic updates that are automatically maintained in journal files, which can result in zone data corruption.

The nsupdate program reads input from a specially formatted file or from standard input. Here is the syntax for the command:

```
nsupdate [-d] [ -y keyname:secret ] [ -k keyfile ] [-v] [filename]
```

## The rndc Tool

The remote daemon control is handy for controlling the name server and debugging problems with the name server. The rndc program can be used to manage the name server securely. A separate configuration file is required for rndc; all communication with the server is authenticated with digital signatures and a shared secret, which is typically stored in a configuration file named /etc/rndc.conf. You will need to generate the secret that is shared between the utility and the name server by using tools such as rndc-keygen (we don't discuss this feature).

Following is the usage for rndc:

```
rndc [-c config] [-s server] [-p port] [-k key-file] [-y key] [-V] command
```

command is one of the following:
- reload Reload configuration file and zones.
- reload zone [class view] reload a single zone.
- refresh zone [class view] Schedule immediate maintenance for a zone.
- reconfig Reload configuration file and new zones only.
- stats Write server statistics to the statistics file.
- querylog Toggle query logging.
- dumpdb Dump cache(s) to the dump file (named_dump.db).
- stop Saving updates to master files and stop the server.
- halt Stop the server without saving pending updates.
```
