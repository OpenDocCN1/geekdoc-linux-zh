
the `<VirtualHost>`. So, when configuring virtual hosts, you need to decide what changes need to be made in each of the virtual host configurations.

The directives either override the configuration given in the primary server or supplement it, depending on the directive. For example, the DocumentRoot directive in a `<VirtualHost>` container overrides the primary server's DocumentRoot, whereas the AddType directive supplements the main server's MIME types.

Now, when a request arrives, Apache uses the IP address and port on which it arrived to find a matching virtual host configuration. If no virtual host matches the address and port, it is handled by the primary server configuration. If it does match a virtual host address, Apache uses the configuration of that virtual server to handle the request.

In the previous example, the virtual host configuration used is the same as the primary server, except that the DocumentRoot is set to `/www/apachehandbook/public/htdocs`, and the ServerName is set to `www.apachehandbook.com`. Directives commonly set in `<VirtualHost>` containers are DocumentRoot, ServerName, ErrorLog, and TransferLog.

You can put almost any configuration directive in the `<VirtualHost>` container, with the exception of ServerType, StartServers, MaxSpareServers, MinSpareServers, MaxRequestPerChild, BindAddress, Listen, PidFile, TypeConfig, ServerRoot, and NameVirtualHost. User and Group may be used inside `<VirtualHost>` containers if the suEXEC wrapper is used.

You can have as many `<VirtualHost>` containers as you want. You can have one or more of your virtual hosts handled by the primary server, or have a `<VirtualHost>` for every available address and port and leave the primary server with no requests to handle.

## Apache configuration for IP-based virtual hosts

Setting up IP-based virtual hosts in a single primary Apache server configuration is very simple. Simply create a `<VirtualHost>` container per virtual IP-address. For example, to create a virtual host called `vhost1.domain.com` (192.168.0.50) with `/www/vhost1/` as the DocumentRoot directory, add the following lines to the `httpd.conf` file:

```
<VirtualHost 192.168.0.50>
DocumentRoot "/www/vhost1/"
ServerName vhost1.domain.com
</VirtualHost>
```

## Apache configuration for name-based virtual hosts

Setting up name-based virtual hosts is also very easy. The first step is to set the `NameVirtualHost` directive to the IP address of the name-based virtual hosts. This directive specifies an IP address that should be used as a target for name-based virtual hosts. For example, suppose you want to set up two virtual hosts, such as `www.client1.com` and `www.client2.com`, on an Apache server that listens to IP address 192.168.0.50. Here is an example configuration for such a setup:

```
NameVirtualHost 192.168.0.50
```

```
<VirtualHost 192.168.0.50>
    ServerName www.client1.com
    DocumentRoot "/www/client1"
</VirtualHost>
```

```
<VirtualHost 192.168.0.50>
    ServerName www.client2.com
    DocumentRoot "/www/client2"
</VirtualHost>
```

You need only a single `NameVirtualHost` directive per IP address for all the name-based virtual hosts using that IP address. When a request comes for one of these virtual hosts from an HTTP/1.1-compliant browser, Apache matches the `ServerName` directive with the host name provided in the `Host` header of the request. Thus, Apache is able to determine which virtual host was requested.

After you create the virtual host configuration for Apache, start (or restart) the Apache server so that the configuration takes effect. Also, don't forget to create any directories that you might be using in a virtual host configuration, before you restart your Apache server.

![](img/f9ec99365f159bfe663f8ac29732663c_356_0.png)

### Tip

Starting with Apache 1.3.x, you can verify your virtual host configuration by running Apache using the `-s` option.

## Using Apache as a proxy server

Proxy support in Apache comes from the `mod_proxy` module. This module is not compiled by default.

### Compiling the proxy module

If you are using the APACII interface to compile and install Apache, then building a new Apache executable with the proxy module is as easy as performing the following steps in your Apache source distribution directory:

- 1. If you are running the `configure` script for the first time, enter the following command:

```
./configure \
--prefix=/dir/where/you/want/to/install/apache \
--enable-module=proxy
```

Conversely, if you have already run the `configure` script to compile Apache, enter the following:

```
./config.status --enable-module=proxy
```

Your previous configuration options will be applied when you create a new configuration file.

- 2. Run the `make` command. If it returns no error messages, run the `make install` command to install the newly compiled Apache executable in the appropriate directory.

### Proxy module directives

The proxy module for Apache comes with the set of directives that you need in order to use the module. All of these directives are usable in both the main server configuration and in any virtual server configuration context.

`ProxyRequests on | off`

This directive allows you to enable or disable the caching proxy service. However, it does not affect the functionality of the `ProxyPass` directive. The default value is off.

`ProxyRemote match remote-proxy-server-URL`

This directive enables you to interface your proxy server with another proxy server. The value of *match* can be either the name of a URL scheme (`http`, `ftp`, and so on) or a partial URL.

*remote-proxy-server-URL* can be `http://remote-proxy-hostname:port`. Currently, only the HTTP protocol is supported. In other words, you can specify only a proxy server that deals with the HTTP protocol; however, you can forward FTP requests from your proxy server to one that supports both HTTP and FTP protocols, as follows:

```
ProxyRemote ftp http://ftp.proxy.nitec.com:8000
```

This sends all FTP requests that come to the local proxy server to `ftp://ftp.proxy.nitec.com`. The requests will be sent via HTTP, so the actual FTP transaction will occur at the remote proxy server.

If you want to forward all proxy requests for a certain Web site to its proxy server directly, you can do that with the `ProxyRemote` directive. For example,

```
ProxyRemote http://www.isp.com  http://web-proxy.isp.com:8000
```

sends all requests that match `www.isp.com` to `web-proxy.isp.com`.

If you want to forward all of your proxy requests to another proxy, however, use the asterisk as the match phrase. For example,

```
ProxyRemote  * http://proxy.domain.com
```

sends all local proxy requests to the proxy server at `proxy.domain.com`.

`ProxyPass relative-URL destination-URL`

This directive enables you to map a Web server's document tree onto your proxy server's document space. For example,

```
ProxyPass  /internet/microsoft  www.formserv.com/
```

The above `ProxyPass` directive, found in the `httpd.conf` file of a proxy server called `proxy.nitec.com`, permits users of the proxy server to access the FormServ Web site using the URL:

```
http://proxy.nitec.com/internet/formserv
```

This directive (**ProxyPass**) makes **proxy.nitec.com** act like a mirror of the **www.formserv.com** Web site. Any request that uses the *relative-URL* will be converted internally into a proxy request for the *destination-URL*.

`ProxyPassReverse relative-URL destination-URL`

This directive is useful when you want to create a reverse proxy server using Apache. In such a reverse proxy setup, this directive fixes the *Location* headers that might be returned by the actual Web server. For example, in the following, **www.nitec.com** is the proxy server that gets all the pages from another server called *realserver.nitec.com*:

```
<VirtualHost 206.171.50.50>
  ServerName www.nitec.com
  ProxyRequests on
  ProxyPass / realserver.nitec.com/
  ProxyPassReverse / realserver.nitec.com/
</VirtualHost>
```

The **ProxyPass** directive enables this feature. However, if a page on *realserver.nitec.com* sends a *Location* header in response, the **ProxyPassReverse** directive fixes it so that the proxy server **www.nitec.com** is not bypassed by the client.

`ProxyBlock partial or full host name . . .`

This directive enables you to block access to a named host or domain.
For example,

```
ProxyBlock gates
```

blocks access to any host that has the word **gates** in its name. This way, access to *http://gates.ms* or *http://gates.friendsofbill.com* will be blocked. You can also specify multiple hosts, as follows:
