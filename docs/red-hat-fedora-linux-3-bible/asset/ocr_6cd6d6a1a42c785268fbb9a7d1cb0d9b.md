The **hierarchy_stoplist** tag indicates that when a certain string of characters appears in a URL, the content should be obtained from the original server and not from a cache peer. In this example, requests for the string **cgi-bin** and the question mark character (?) are all forwarded to the originating server.

```
acl QUERY urlpath_regex cgi-bin \
no_cache deny QUERY
```

The preceding two lines can be used to cause URLs containing certain characters to never be cached. These go along with the previous line by not caching URLs containing the same strings (**cgi-bin** and ?) that are always sought from the original server.

```
acl all src 0.0.0.0/0:0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

The **acl** tags are used to create access control lists. The first line above creates an access control list called **all** that includes all IP addresses. The next **acl** line assigns the **manager** **acl** to handle the **cache_object** protocol. The **localhost** source is assigned to the IP address of 127.0.0.1.

The next several entries define how particular ports are handled and how access is assigned to HTTP and ICP services.

```
acl SSL_ports port 443 563
acl Safe_ports port 80   # http
acl Safe_ports port 21   # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70   # gopher
acl Safe_ports port 210  # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280  # http-mgmt
acl Safe_ports port 488  # gss-http
acl Safe_ports port 591  # filemaker
acl Safe_ports port 777  # multiling http
acl CONNECT method CONNECT
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
http_reply_access allow all
icp_access allow all
```

The following sections describe these settings in more detail, as well as other tags you might want to set in your **squid.conf** file. By default, no clients can use the Squid proxy server, so you at least want to define which computers can access proxy services.