This example specifies that the default domain name to append to unqualified names (i.e., hostnames supplied without a domain) is math.s.wu.edu.au and that if the host is not found in that domain to also try the wu.edu.au domain directly. Two nameservers entry are supplied, each of which may be called upon by the name resolver code to resolve the name.

# /etc/host.conf

The /etc/host.conf file is where you configure some items that govern the behavior of the name resolver code. The format of this file is described in detail in the “resolv+” man page. In nearly all circumstances the following example will work for you:

```
order hosts,bind
multi on
```

This configuration tells the name resolver to check the /etc/hosts file before attempting to query a nameserver and to return all valid addresses for a host found in the /etc/hosts file instead of just the first.

# /etc/hosts

The /etc/hosts file is where you put the name and IP address of local hosts. If you place a host in this file, then you do not need to query the domain name server to get its IP Address. The disadvantage of doing this is that you must keep this file up-to-date yourself if the IP address for that host changes. In a well-managed system the only hostnames that usually appear in this file are an entry for the loopback interface and the local host name.

```
# /etc/hosts
127.0.0.1 localhost loopback
192.168.0.1 this.host.name
```

You may specify more than one hostname per line as demonstrated by the first entry, which is a standard entry for the loopback interface.

# Running a Name Server

If you want to run a local nameserver, you can do it easily. Please refer to the DNS-HOWTO and to any documents included in your version of BIND (Berkeley Internet Name Domain).