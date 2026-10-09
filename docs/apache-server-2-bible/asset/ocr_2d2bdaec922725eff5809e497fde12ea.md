# ProxyRequests

ProxyRequests allows you to enable or disable the caching proxy service. However, it does not affect the functionality of the ProxyPass directive.

+   Syntax: ProxyRequests On | Off
+   Default setting: ProxyRequests Off
+   Context: Server config, virtual host

# ProxyRemote

ProxyRemote enables you to interlace your proxy server with another proxy server.

+   Syntax: ProxyRemote match remote_proxy_server_URL
+   Default setting: None
+   Context: Server config, virtual host

The value of match can be one of the following:

+   The name of an URL scheme that the remote server supports
+   A partial URL, for which the remote server should be used
+   To indicate the server should be contacted for all requests

The remote_proxy_server_URL can be specified as http://hostname::port. Note that, currently, only the HTTP protocol is supported. In other words, you can only specify a proxy server that deals with the HTTP protocol; however, you can forward FTP requests from your proxy server to one that supports both HTTP and FTP protocols as follows:

```
ProxyRemote ftp http://ftp.proxy.evoknow.com:8000
```

This sends all FTP requests that come to the local proxy server to ftp://ftp.proxy.evoknow.com. The requests are sent via HTTP, so the actual FTP transaction occurs at the remote proxy server.

If you just want to forward all proxy requests for a certain Web site to its proxy server directly, you can do that with this directive. For example:

```
ProxyRemote http://www.bigisp.com/ http://web-proxy.bigisp.com:8000
```