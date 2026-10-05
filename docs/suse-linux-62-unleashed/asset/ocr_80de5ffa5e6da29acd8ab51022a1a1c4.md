# TCP/IP and Network Management
CHAPTER 7

With this configuration, all names except network names will be looked up first in /var/db
(for efficiency). If not found there, it will be looked up in the corresponding /etc files.
There are quite a few databases that could be looked up by NIS if an appropriate entry
exists in the corresponding database.

# Configure the DNS Client: /etc/resolv.conf

The /etc/resolv.conf file configures the DNS client. It contains the host's domain name
search order and the addresses of the DNS servers. Each line should contain a keyword and
one or more parameters separated by spaces. The following keywords are valid:

| Keyword | Meaning |
| --- | --- |
| nameserver | Its single parameter indicates the IP address of the DNS server.
There may be up to three nameserver lines, each with a single IP
address. nameservers will be queried in the order they appear in
the file. nameservers after the first one will only be queried if the
first nameserver doesn't respond.
| domain | Its single parameter indicates the host's domain name. This is used
by several programs, such as the email system, and is also used
when doing a DNS query for a host with no domain name (with no
periods, for example). If there's no domain name, the hostname
will be used, removing everything before the first dot.
| search | Its multiple parameters indicate the domain name search order. If a
query is made for a host with no domain name, the host will be
looked up consecutively in each of the domains indicated by
the keyword. Note that domain and search are mutually
exclusive; if both appear, the last one that appears is used.
| sortlist | Allows sorting the returned domain names in a specific order. Its
parameters are specified via network/mask pairs, allowing for
arbitrary sorting order.

![](bbox=[0.843, 0.273, 0.953, 0.443])

There is no generic default /etc/resolv.conf file provided with Linux. Its contents are
built dynamically depending on options given at installation time. This is a sample /etc/
resolv.conf file:

```
search my.domain.com other.domain.com
ameserver 10.1.1.1
nameserver 10.10.10.1
sortlist 10.1.1.0/255.255.255 10.0.0.0/255.255.255
```

This file indicates that unqualified hosts will be searched first as host my.domain.com and
then as other.domain.com. The nameserver at IP address 10.1.1.1 will be
contacted first. If that server doesn't answer after a timeout, the server at 10.10.10.1 will