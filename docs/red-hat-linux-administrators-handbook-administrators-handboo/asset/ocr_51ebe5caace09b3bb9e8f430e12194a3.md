This directive is useful when you want to create a reverse proxy server using Apache. In such a reverse proxy setup, this directive fixes the Location headers that might be returned by the actual Web server. For example, in the following, www.nitec.com is the proxy server that gets all the pages from another server called realserver.nitec.com:

```
<VirtualHost 206.171.50.50>
ServerName www.nitec.com
ProxyRequests on
ProxyPass / realserver.nitec.com/
ProxyPassReverse / realserver.nitec.com/
</VirtualHost>
```

The ProxyPass directive enables this feature. However, if a page on realserver.nitec.com sends a Location header in response, the ProxyPassReverse directive fixes it so that the proxy server www.nitec.com is not bypassed by the client.

# ProxyBlock partial or full host name . . .

This directive enables you to block access to a named host or domain. For example,

```
ProxyBlock gates
```

blocks access to any host that has the word "gates" in its name. This way, access to http://gates.ms.com or http://gates.friendsof-bill.com will be blocked. You also can specify multiple hosts, as follows:

```
ProxyBlock apple orange.com banana.com
```

This directive blocks all access to any host that matches any of the preceding words or domain names. The mod_proxy module attempts to determine the IP addresses for these hosts during server startup and caches them for matching later.

To block access to all hosts, use the following:

```
ProxyBlock *
```

This effectively disables your proxy server.

```
NoProxy Domain name | Subnet | IP Address | Hostname
```