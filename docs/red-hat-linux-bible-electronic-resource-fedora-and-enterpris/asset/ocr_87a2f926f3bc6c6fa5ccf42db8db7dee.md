The next several entries define how particular ports are handled and how access is assigned to HTTP and ICP services.

```
acl SSL_ports port 443 563
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
acl Safe_ports port 777 # multiling http
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

The following sections describe these settings in more detail, as well as other tags you may want to set in your squid.conf file. By default, no clients can use the squid proxy server, so you at least want to define which computers can access proxy services.

To make sure that this simple Squid configuration is working, follow the procedure below:

+   1. On the Squid server, restart the squid daemon. To do this, either reboot or type /etc/init.d/squid restart. (If Squid isn't running, use start instead of restart.)
+   2. On the Squid server, start your connection to the Internet (if it is not already up).
+   3. On a client computer on your network, set up Mozilla (or another Web browser) to use the Squid server as a proxy server (described later in this chapter). (In Mozilla, choose Edit \u2192 Preferences \u2192 Advanced \u2192 Proxies, then choose Manual proxy configuration and add the Squid server's computer name and, by default, port 3128 to each protocol.)
+   4. On the client computer, try to open any Web page on the Internet with the browser you just configured.

If the Web page doesn't appear, see the Squid debugging section for how to fix the problem.

# Modifying the Squid configuration file

If you want to set up a more complex set of access permissions for Squid, you should start with the default squid.conf configuration file (described earlier).