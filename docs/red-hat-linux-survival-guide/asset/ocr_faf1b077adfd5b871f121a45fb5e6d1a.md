Here is an example of an /etc/hosts file:

```
206.171.50.50 picaso.evoknow.com picaso
127.0.0.1 localhost localhost
```

The resolver can use this file to resolve an address when the remote DNS servers are not available. Also, if you have a small network and do not want to run a local DNS server, you may use this file to resolve local host names. However, when both the remote DNS server and the /etc/hosts file are available, the resolver needs to know in which order to process DNS queries. You can set the order in the /etc/host.conf file using the order directive. For example:

```
order hosts,bind
```

If your /etc/host.conf file has this order directive, then the resolver first attempts to use the /etc/hosts file to service the query. If the file does not contain an entry that can be used, the DNS servers specified in the /etc/resolv.conf file are used.

![](bbox=[0.06, 0.57, 0.15, 0.66])

If you have a large user base, you can improve DNS-related performance by using a local DNS server over an /etc/hosts file, because reading the file for each new DNS request can be quite slow.

After you’ve set up the files just described, your DNS resolver configuration is complete. The easiest way to test your DNS configuration is to try to ping a computer on the Internet. If the ping program fails because of an unknown host name, double-check your DNS resolver configuration for typos.

Running your own DNS server has quite a few administrative benefits. For example, if you own one or more Internet domains, you can add, delete, or modify DNS records as you please. In the following section you learn how to set up a DNS server on your Red Hat Linux system.

# Installing the BIND DNS Server

Red Hat Linux comes with the Berkeley Internet Name Domain (BIND) server software. If you have not installed it during the operating system