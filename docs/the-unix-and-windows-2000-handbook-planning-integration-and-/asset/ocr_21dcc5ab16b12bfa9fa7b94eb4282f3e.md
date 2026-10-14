The first line defines the domain name to append to form a complete hostname to pass to the DNS server. The next two lines define the IP address of the DNS server to use for hostname resolution. Only IP addresses are valid here; never use the hostname of the DNS server. You add redundancy to your system by adding multiple DNS servers. DNS servers will be queried in the order in which you place nameserver entries. If the first server doesn’t respond, your system will query the second server, and so on.

# SEARCH DOMAINS

The addition of search domains to your `/etc/resolv.conf` file allows you to integrate additional domains into hostname resolution. Search domains provide an option to name resolution that is unnecessary if your system will live within a single domain. However, if your system will be part of a large network with multiple domains, using the search domain option can ease your administrative tasks as well as make navigating the network easier for your users.

```
mars:> cat /etc/resolv.conf

domain yourdomain.edu

search domain1,domain2,domain3,domain4

nameserver 192.168.3.49

nameserver 192.168.3.74
```

By adding the search line, hostname lookups will append each domain in the search line to the hostname you are attempting to resolve. For example, if you were trying to resolve the name `rover`, the system would request from the DNS server the address of `rover.yourdomain.edu`, `rover.domain1`, `rover.domain2`, etc. until the DNS server returned a valid IP address, or returned an error message that the host doesn’t exist.

Be careful. Adding a large number of search domains can slow down hostname resolution. Also, attempt to optimize the search line so that more popular names come first.

# NIS+ DOMAIN NAME

If you are using Network Information Services (NIS+) for name services, make sure you know your NIS+ domain before you begin your installation. While NIS+ will be discussed in more detail in Chapter 7, “Directory Services” in many cases you will be asked at install time if you are going to use NIS+ for naming services. Double-check that you have the correct domain