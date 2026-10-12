![](bbox=[0.08, 0.17, 0.18, 0.28])

Many tools are available for manually querying name servers, including dig. If you would like to have a few commonly used query tools, install the bind-utils RPM distribution from your Red Hat CD-ROM. The bind-utils distribution comes with dig, dnsquery, host, nslookup, and more.

Say that you just registered a new domain with Internic and have already set up the necessary DNS configuration on your name server. After restarting the name server, you want to test the configuration via dig. You can run dig using the following syntax:

```
dig @nameserver domain [query_type]
```

The nameserver can be a DNS server's host name or IP address. If you're running dig on the same machine as the DNS server you wish to test, you don't need to specify the DNS server using @nameserver as long as your /etc/resolv.conf has a line that makes the target DNS server the default name server for that machine. The domain in the above syntax is the domain name or the host name for which you want to find a DNS record of type query_type. By default query_type is set to A (Address) record. For example:

```
dig @ns.aminews.com evoknow.com ns
```

Here the DNS server ns.aminews.com is asked to locate NS record for evoknow.com domain. Lets look at another example:

```
dig www.evoknow.com A
```

Here the default DNS server (i.e., the one set in /etc/resolv.conf) is being asked to locate the A (Address) record for a host name called www.evoknow.com.

As you can see, you can use dig to dig up your DNS configuration quite easily by pointing it to the right name server and asking for the query types that you wish to check.