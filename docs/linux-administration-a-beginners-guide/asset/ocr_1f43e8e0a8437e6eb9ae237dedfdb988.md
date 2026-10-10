Under Linux, the client side of DNS is handled by the resolver. This is actually part of a library of C programming functions that get linked to a program when the program is started. Because all of this happens automatically and transparently, the user doesn't have to know anything about it. It's simply a little bit of magic that let's them start browsing the Internet.

From the systems administration perspective, configuring the DNS client isn't magic, but it's very straightforward. There are only two files involved: /etc/resolv.conf and /etc/nsswitch.conf.

# The /etc/resolv.conf file

The /etc/resolv.conf file contains the information necessary for the client to know what its local DNS server is. (Every site should have, at the very least, its own caching DNS server.) This file has two lines: the first indicates the default search domain, and the second line indicates the IP address of the host's name server.

The default search domain applies mostly to sites that have their own local servers. When the default search domain is specified, the client files will automatically append this domain name to the requested site and check that first. For example, if we specify our default domain to be yahoo.com and then try to connect to the host name my, the client software will automatically try contacting my.yahoo.com. Using the same default, if we try to contact the host www.stat.net, the software will try www.stat.net.yahoo.com (a perfectly legal host name), find that it doesn't exist, and then try stat.net (alone which does exist).

You may, of course, supply multiple default domains. However, doing so will slow the query process a bit because each domain will need to be checked. For instance, if both yahoo.com and stanford.edu are specified, and we perform a query on www.stat.net, we'll get three queries: www.statnet.yahoo.com, www.stat.net.stanford.edu, and www.stat.net.

The format of the /etc/resolv.conf file is as follows:

```
search domainname

nameserver IP-address
```

where domainname is the default domain name to search, and IP-address is the IP address of your DNS server. For example, here's my /etc/resolv.conf:

```
search planetoid.org

nameserver 127.0.0.1
```

Thus when I contact zaphod.planetoid.org, I only need to specify zaphod as the host name. Since I run a name server on my own machine, I specify the local host address.

# The /etc/nsswitch.conf file

The /etc/nsswitch.conf file tells the system where it should look up certain kinds of configuration information (services). When multiple locations are identified, the