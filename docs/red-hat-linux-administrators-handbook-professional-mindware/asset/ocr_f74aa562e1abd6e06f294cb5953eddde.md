```
CacheRoot /www/cache
CacheDefaultExpire 24
```

This makes a proxy server a mirror of the www.apache.org Web site. For example, this configuration turns my proxy server blackhole.nitec.com into a www.apache.org mirror. Users who enter http://black hole.nitec.com as the URL receive the Apache mirror’s index page just as if they had gone to www.apache.org.

![](bbox=[0.05, 0.32, 0.15, 0.39])

# Caution

Before you mirror someone else’s Web site, you must get their permission, because copyright issues may be involved.

# Creating a reverse proxy server

Reverse proxy servers are needed when the real HTTP/FTP server is behind a firewall or when some load-balancing scheme needs to be in place to speed up or distribute delivery of the content. Creating a reverse proxy server is quite easy with the latest proxy module found in Apache 1.3.x. Suppose you have a Web server with host name realserver.your company.com and you want to have everyone visit it via a reverse proxy server called www.yourcompany.com (11.22.33.44). You can create the following virtual host on .yourcompany.com server:

```
<VirtualHost 11.22.33.44>
ServerName www.yourcompany.com
ProxyPass / realserver.yourcompany.com/
ProxyPassReverse / realserver.yourcompany.com/
CacheRoot /www/cache
CacheDefaultExpire 24
</VirtualHost>
```

This makes the proxy server a reverse proxy for realserver.your company.com. To your visitors, it appears as if they are accessing www. yourcompany.com.