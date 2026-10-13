+   - IP address-based virtual hosting (or hardware virtual hosting) in which the Web server has multiple IP addresses and a different IP address is associated with each site.
+   - Hostname-based virtual hosting (or software virtual hosting) in which the Web server responds to a single IP address but multiple hostnames are associated with that address and each hostname is associated with a different Web site on the server.

IP address-based hosting provides the advantage that the client does not need to provide any special information to the server in order for the server to select and serve the correct site. However, because IP addresses are increasingly in short supply, this option is unattractive for servers offering Web sites on the public Internet.

Name-based virtual hosting requires that the client provide a host header field in which the hostname of the desired site is indicated. This is an HTTP 1.1 feature supported by all newer browsers, but some older browsers do not support this. With these browsers, the server will receive a request on its IP address but have no information to determine which site to serve. Nonetheless, software virtual hosting of this type is increasingly the norm because it does not strain the availability of IP addresses unnecessarily. In this chapter we will consider implementation of hostname-based virtual hosting.

Implementing name-based virtual hosting requires three steps:

+   - Creating DNS entries for each site
+   - Creating a directory hierarchy for the sites
+   - Configuring Apache to serve each site

# CREATING DNS ENTRIES FOR EACH SITE

A Web server on the Internet needs a primary A record for itself, which indicates the primary domain name for the server. If your Web server’s primary domain name is www.my.domain and its IP address is 1.2.3.4, the DNS A record for the server would be:

```
www.my.domain.   IN   A   1.2.3.4
```

For each additional site you want to host on the system using name-based virtual hosting, you must create a canonical name (CNAME) record which serves as an alias for the server. For instance, to associate a second domain name, fun.my.domain, with the same server you would use the following CNAME record:

```
fun.my.domain.   IN   CNAME   www.my.domain.
```

Even if you want to create virtual hosts in domains other than the domain of the primary hostname, you can still use CNAME records. For instance, you can alias www.another.domain to www.my.domain using the following CNAME entries in the DNS records for another.domain:

```
www.another.domain.   IN   CNAME   www.my.domain.
```

Complete details of DNS management and the creation and editing of DNS zone files is discussed in Chapter 22, “DNS.”