# 652 Part IV: Fedora Network and Server Setup

The acl tags are used to create access control lists. The all acl is defined to include all IP addresses. The next acl line assigns the manager acl to handle the cache_object protocol. The localhost source is assigned to the IP address of 127.0.0.1.

```
access_log /var/log/squid/access.log squid # implicit
```

The preceding line identifies the location of the Squid access.log file. As the name implies, this file contains messages about requests to access the Squid server.

Squid includes default settings for how long different types of content in cache are still considered to be fresh. The following refresh_pattern values are included in the squid.conf file:

```
```
refresh_pattern   ^ftp:   1440    20%   10080
refresh_pattern   ^gopher:  1440    0%   1440
refresh_pattern   .      0      20%   4320
```
```

In the code just shown, all lines that begin (^) with ftp or gopher are set to expire in 1440 minutes. The percentage of the object’s age during which it is considered to be fresh is shown in the next column (20%, 0%, and 20%). The last column indicates the maximum number of minutes during which the object will be considered fresh. The next several entries define how particular ports are handled and how access is assigned to HTTP and ICP services.

```
```
acl SSL_ports port 443
acl Safe_ports port 80     # http
acl Safe_ports port 21     # ftp
acl Safe_ports port 443    # https
acl Safe_ports port 70     # gopher
acl Safe_ports port 210    # wais
acl Safe_ports port 1025-65535  # unregistered ports
acl Safe_ports port 280    # http-mgmt
acl Safe_ports port 488    # gss-http
acl Safe_ports port 591    # filemaker
acl Safe_ports port 777    # multi-iling http
acl CONNECT method CONNECT
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost # localnet is defined as private ip networks
http_access allow localnet
http_access deny all
http_reply access allow all
icp_access allow all
```
```