# **Configuring DNS**

Recall that DNS is a hierarchical namespace used to identify computers on large TCP/IP networks such as the Internet. Each part of this namespace is called a **zone** and DNS servers contain all host name information for a zone. DNS servers typically resolve FQDNs to IP addresses (called a **forward lookup**), but can also resolve IP addresses to FQDNs (called a **reverse lookup**).

When you contact a Web server on the Internet using a Web browser, the Web browser performs a forward lookup of the FQDN such that it can contact the IP address of the Web server. This forward lookup can be performed by a DNS server, or series of DNS servers. The whole process used to resolve the FQDN `www.linux.org` is illustrated in Figure 15-2.

![](bbox=[0.1, 0.33, 0.95, 0.65])

In the first step from Figure 15-2, the Linux computer sends a forward lookup request for `www.linux.org` to the DNS server that is configured in `/etc/resolv.conf`; this is typically the DNS server at your ISP. If the ISP DNS server has recently resolved the FQDN and placed the result in its local DNS cache, you receive the response immediately (called an **iterative query**). If it has not, the ISP DNS server normally contacts the DNS server for the `.org` top-level zone (Step 2) and repeats the forward lookup request for `www.linux.org` (called a **recursive query**). The `.org` DNS server will not contain the IP address for the `www.linux.org` computer in its zone, but will reply with the IP address of the DNS server for the `linux.org` zone (Step 3).

> **NOTE**
> 
> All DNS servers contain a **DNS cache file** that contains the IP addresses of DNS servers that hold top-level DNS zones.