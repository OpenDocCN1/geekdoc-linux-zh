```
# include all IPs from 192.168.0.0 to 192.168.0.255
acl internal src 192.168.0.0/24

# include all IPs from 192.168.0.0 to 192.168.0.255
# and all IPs from 10.0.0.0 to 10.255.255.255
acl internal src 192.168.0.0/24 10.0.0.0/8
```

When you have your ACL lines in place, you can put together appropriate `http_access` lines. For example, you might want to use a multilayered access system so that certain users (for example, company directors) have full access, whereas others are filtered. For example:

```
http_access allow directors
http_access deny hotmail
http_access deny zipfiles
http_access allow internal lunchtimes
http_access deny all
```

Because Squid matches those lines in order, directors will have full, unfiltered access to the Web. If the client IP address is not in the directors list, the two deny lines are processed so that the user cannot download `.zip` files or read online mail at Hotmail. After blocking those two types of requests, the `allow` on the fourth line allows internal users to access the Web, as long as they do so only at lunch time. The last line (which is highly recommended) blocks all other users from the proxy.

# Reference

+   - http://www.squid-cache.org—The home page of the Squid Web Proxy Cache.
+   - http://squid-docs.sourceforge.net/latest/book-full.html—The home page of *Squid: A User's Guide*, a free online book about Squid.
+   - http://www.lacq.org/docs/server/netproxy-squid.html—A brief online guide to configuring a local Squid server.
+   - http://squid.visolve.com/squid/index.html/—The home page of a company that can provide commercial support and deployment of Squid.
+   - http://www.visolve.com/squid/reverseproxy.htm—Visolve's guide to setting up Squid to reverse proxy to cache a local web server for external visitors.

As well as these URLs, there are two excellent books on the topic of web caching. The first is *Squid: The Definitive Guide* (O'Reilly) by Duane Wessels, ISBN: 0-596-00162-2. The second is *Web Caching* (O'Reilly) also by Duane Wessels, ISBN: 1-56592-536-X.

Of the two, the former is more practical and covers the Squid server in depth. The latter is more theoretical, discussing how caching is implemented. Wessels is one of the leading developers on Squid, so both books are of impeccable technical accuracy.