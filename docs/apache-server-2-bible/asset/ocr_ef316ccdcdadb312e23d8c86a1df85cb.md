# **Scenario 1: Connecting a private IP network to the Internet**

In this scenario, only one computer on this network has an Internet-routable IP address assigned to it, as shown in **Figure 10-3**. This computer runs the Apache proxy server with the `ProxyRequest` set to `On`, and no additional proxy configuration is needed. The proxy server services all requests.

![](bbox=[0.15, 0.32, 0.85, 0.59])

In such a configuration, the proxy server needs to be multihomed; in other words, it needs to have access to both the nonroutable private network (`192.168.1.0`) and the routable IP network (`206.171.50.0`). In a way, this proxy acts as a firewall for the private IP network although the chosen nonroutable IP pool does that already. The proxy permits the hosts to get access to Internet services, such as the Web, FTP, and so on.

# **Scenario 2: Caching remote Web sites**

Because a great deal of Web content on both the Internet and intranets is likely to be static, caching them on a local proxy server could save valuable network bandwidth. A cache-enabled proxy server fetches requested documents only when the cache contains an expired document or when the requested document is not present in the cache. To enable caching on your proxy server, you need to specify caching directives inside the special directory container. For example:

```
```apache
<Directory proxy:*>  CacheRoot /www/cache
  CacheSize 1024
  CacheMaxExpire 24
</Directory>
```
```