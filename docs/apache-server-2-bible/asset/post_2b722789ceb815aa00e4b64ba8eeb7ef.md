
## CacheDirLength

When disk caching is on, Apache creates subdirectories in the directory specified by the *CacheRoot* directive. This directive specifies the number of characters used in creating the subdirectory names. You really do not need to change the default for this directive. For curious users who want to know how or why these subdirectories are created, a simplified answer follows.

- **Syntax:** CacheDirLength *length*
- **Default setting:** CacheDirLength 1
- **Context:** Server config, virtual host

Apache uses a hashing scheme when creating the path and filename for a URL's data to be cached. For example, when you have caching turned on and access a URL (such as *www.microsoft.com*) via your proxy Apache server, the server hashes this URL so that it can later retrieve the data quickly. This hash could look like 1Y5RxSmB2OQ_HkqkTuXeqvw. If the defaults are used for both the CacheDirLength and CacheDirLevels directives, Apache stores the data found on *www.microsoft.com* in a file called:

%CacheRoot%/*/1/Y/5/RxSmB2OQ_HkqkTuXeqvw

Here %CacheRoot% is the directory specified by the *CacheRoot* directive. The *1/Y/S* directories are created because of the default value of the *CacheDirLevels* directive. When this document is requested again using the same URL, Apache need only recalculate the hash to retrieve the page from the specified path.

## CacheDirLevels

CacheDirLevels specifies the number of subdirectories that Apache will create to store cache data files. See the previous section for related information.

- **Syntax:** CacheDirLevels *levels*
- **Default setting:** CacheDirLevels 3
- **Context:** Server config, virtual host

## CacheDefaultExpire

CacheDefaultExpire provides a default time (in hours) that is used to expire a cached file when the last modification time of the file is unknown. *CacheMaxExpire* does not override this setting.

- **Syntax:** CacheDefaultExpire *hours*
- **Default setting:** CacheDefaultExpire 1
- **Context:** Server config, virtual host

## NoCache

- **Syntax:** NoCache _Domain_name_ | _Subnet_ | _IP_Address_ | _Hostname_ . . .
- **Default setting:** None
- **Context:** Server config, virtual host

The NoCache directive specifies a list of hosts, domain names, and IP addresses, separated by spaces, for which no caching is performed. This directive should be used to disable caching of local Web servers on an intranet. Note that the proxy server also matches partial names of a host. If you want to disable caching altogether, use the following:

```apache
NoCache *
```

# Configuring an Apache Proxy Server

In this section I show you how you can configure Apache (with _mod_proxy_) as a forward proxy server. After you have the _mod_proxy_ module compiled into Apache (as discussed earlier), setting up a proxy server is quite easy.

To enable the proxy server, you need to set the _ProxyRequests_ to _On_ in an _httpd.conf_ file. Any additional configuration depends on what you want to do with your proxy server. Regardless of what you decide to do with the proxy server, any directives that you want to use to control the proxy server’s behavior should go inside a special `<Directory ...>` container that looks like the following:

```apache
<Directory proxy:*>
<.dir>
</Directory>
```

The asterisk is a wild card for the requested URL. In other words, when a request for _www.evoknow.com_ is processed by the Apache server, it looks like:

```apache
<Directory proxy:http://www.evoknow.com>
<.dir>
</Directory>
```

You can also use the `<Directory ~ /RE/>` container, which uses regular expressions that allows you greater flexibility in defining the proxy configuration. For example:

```apache
<Directory ~ proxy:http://[a-z]+.*/.*>
<.dir>
</Directory>
```

Now let’s look at a few commonly used proxy configurations.

## Scenario 1: Connecting a private IP network to the Internet

In this scenario, only one computer on this network has an Internet-routable IP address assigned to it, as shown in **Figure 10-3**. This computer runs the Apache proxy server with the `ProxyRequests` set to `On`, and no additional proxy configuration is needed. The proxy server services all requests.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_306_0.png)

In such a configuration, the proxy server needs to be multihomed; in other words, it needs to have access to both the nonroutable private network (`192.168.1.0`) and the routable IP network (`206.171.50.0`). In a way, this proxy acts as a firewall for the private IP network although the chosen nonroutable IP pool does that already. The proxy permits the hosts to get access to Internet services, such as the Web, FTP, and so on.

## Scenario 2: Caching remote Web sites

Because a great deal of Web content on both the Internet and intranets is likely to be static, caching them on a local proxy server could save valuable network bandwidth. A cache-enabled proxy server fetches requested documents only when the cache contains an expired document or when the requested document is not present in the cache. To enable caching on your proxy server, you need to specify caching directives inside the special directory container. For example:

```apache
<Directory proxy:*>
CacheRoot /www/cache
CacheSize 1024
CacheMaxExpire 24
</Directory>
```

This configuration defines a caching proxy server that writes cache files to the `/www/cache` directory. It is permitted to write 1024K of data (1MB) and the cache must expire after each day (24 hours).

If you do not want to permit outsiders to abuse your proxy server, you can restrict proxy server access either by host or by username/password authentication.

To control which hosts have access to the proxy server, you can create a configuration, such as the following:

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
order deny,allow
deny from all
allow from myhost.evoknow.com
</Directory>
```

This configuration denies access to all but `myhost.evoknow.com`. If you want to use username/password authentication, you can use something similar to the following:

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
AuthUserFile /path/to/proxy/.htpasswd
require valid-user
</Directory>
```

**Cross-Reference** If you are not sure how to create the necessary password files, see Chapter 7.

It is also possible to restrict access for a protocol. For example:

```apache
<Directory proxy:http:>
.
</Directory>
```

enables you to control how HTTP requests are processed by your proxy server. Similarly, you can use the following to control how the proxy server handles each protocol:

```apache
<Directory proxy:ftp:*>
.
</Directory>
```

or

```apache
<Directory proxy:https:*>
...
</Directory>
```

You can also create a virtual host exclusively for proxy server. In that case, the directives should go inside the proxy host’s `<VirtualHost>` container:

```apache
<VirtualHost proxy.host.com:*>
...
</VirtualHost>
```

## Scenario 3: Mirroring a Web site

A mirror Web site is a local copy of a remote Web site. For example, if you wanted to mirror the `www.apache.org` Web site so that your users can connect to your mirror site for quick access to Apache information, you can use the proxy server to create such a mirror, as follows:

```apache
ProxyPass / www.apache.org/
CacheRoot /www/cache
CacheDefaultExpire 24
```

This makes a proxy server a mirror of the `www.apache.org` Web site. For example, this configuration turns my proxy server `blackhole.evoknow.com` into an Apache mirror. When a user enters `http://blackhole.evoknow.com` as the URL, the user receives the Apache mirror’s index page as if she had gone to `www.apache.org`.

Before you mirror someone else’s Web site, it is important that you get permission, as there may be copyright issues involved.

# Setting Up Web Browsers to use a Proxy

After your proxy server is configured, you are ready to set up Web browsers on your client hosts. The popular Web browsers make it quite easy to use proxy servers. In the following sections, I show you how to configure Netscape Navigator 6 and Microsoft Internet Explorer (IE) 5.5 for proxy. There are two ways to set up a proxy server for these browsers: manual or automatic proxy configuration.

Manually configuring Web browsers for proxy is not difficult. However, if you have a lot of user computers that need to be configured, this could become a big hassle every time you needed to change your proxy configuration. This is where automatic proxy configuration for browsers comes in handy.

## Manual proxy configuration

You want to do manual proxy configuration in situations in which you have only a few client machines and your proxy configurations do not change often. If your
