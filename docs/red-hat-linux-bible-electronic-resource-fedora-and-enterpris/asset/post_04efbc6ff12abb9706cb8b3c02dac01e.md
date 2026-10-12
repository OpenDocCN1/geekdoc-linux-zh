
# handle known problems with browser implementations.
#

BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\.0" force-response-1.0
BrowserMatch "Java/1\\.0" force-response-1.0
BrowserMatch "JDK/1\\.0" force-response-1.0
#
# The following directive disables redirects on non-GET requests for
# a directory that does not include the trailing slash. This fixes a
# problem with Microsoft WebFolders which does not appropriately handle
# redirects for folders with DAV methods.
# Same deal with Apple's DAV filesystem and Gnome VFS support for DAV.
#

BrowserMatch "Microsoft Data Access Internet Publishing Provider" redirect-carefully
BrowserMatch "^WebDrive" redirect-carefully
BrowserMatch "^WebDAVFS/1.\[012\]" redirect-carefully
BrowserMatch "^gnome-vfs" redirect-carefully

The BrowserMatch directive enables you to set environment variables based on the contents of the User-agent header field. The force-response-1.0 variable causes a HTTP/1.0 response, indicating that the browser cannot support basic HTTP operations.

> **NOTE:** If you are following the httpd.conf file, you notice that we are skipping descriptions of the server-status lines and server-info lines. They are described later in the "Monitoring Server Activities" section.

## Enabling proxy and caching services

Proxy and caching services are turned off by default. You can turn them on by uncommenting several values, presented below:

```
#
# Proxy Server directives. Uncomment the following lines to
# enable the proxy server:
#
#<IfModule mod_proxy.c>
# ProxyRequests On
#
#<Proxy:*>
# Order deny,allow
# Deny from all
# Allow from .example.com
#</Proxy>
#
# Enable/disable the handling of HTTP/1.1 "Via:" headers.
# ("Full" adds server version; "Block" removes outgoing Via: headers)
# Set to one of: Off | On | Full | Block
#
#ProxyVia On

# To enable a cache of proxied content, uncomment the following lines.
# See http://httpd.apache.org/docs-2.0/mod/mod_cache.html for more
details.
#
#<IfModule mod_disk_cache.c>
# CacheEnable disk /
# CacheRoot "/var/cache/mod_proxy"
# CacheSize 500
#</IfModule>

#</IfModule>
# End of proxy directives.
```

Apache can function as a proxy server, a caching server, or a combination of the two. If ProxyRequests is set to off, the server will simply cache files without acting as a proxy. If CacheRoot (which specifies the directory used to contain the cache files) is undefined, no caching will be performed. Both proxy and caching services are off (commented out) by default.

If you turn on caching, the CacheRoot should exist on a file system with enough free space to accommodate the cache, which is limited by the CacheSize directive. However, you should have 20 to 40 percent more space available in the file system because cache cleanup (to maintain the CacheSize, in kilobytes) occurs only periodically (which you can set using the CacheGcInterval directive).

You can add other directives to this example to enable other caching features. The CacheMaxExpire directive can indicate the maximum number of hours that a document will exist in the cache without checking the original document for modifications. The CacheLastModifiedFactor applies to documents that do not have an expiration time, even though the protocol would support one. To formulate an expiration date, the factor (a floating-point number) is multiplied by the number of hours since the document’s last modification. For example, if the document were modified three days ago and the CacheLastModifiedFactor were 0.25, the document would expire from the cache in 18 hours (as long as this value is still below the value of CacheMaxExpire).

The CacheDefaultExpire directive (specifying the number of hours before a document expires) applies to documents received via protocols that do not support expiration times. The NoCache directive contains a space-separated list of IP addresses, host names, or keywords in host names that should not have documents cached.

Here’s how the caching server behaves if you uncomment the Cache lines above:

- The cached files would exist in `/var/cache/mod_proxy`.
- Cache size is limited to 500 Kbytes.

You may want to allow a much larger `CacheSize`, and possibly set a short `CacheGCInterval`, but otherwise the supplied values are reasonable. The `CacheGCInterval` value can be a floating-point number (for example, 1.25 indicates 75 minutes).

### Configuring virtual hosting

If you have one Web server computer, but more than one domain that you want to serve with that computer, you can set up Apache to do virtual hosting. With virtual hosting, a single IP address can be the access point for multiple domain names.

With virtual hosting, when a request comes into your Apache server from a Web browser through a particular IP address on your computer, Apache checks the domain name being requested and displays the content associated with that domain name. As an administrator of a Web server that supports virtual hosting, you must make sure that everything that needs to be configured for that virtual server is set up properly (you must define such things as locations for the Web content, log files, administrative contact, and so on).

Virtual hosting is defined with the `VirtualHost` tags. Information related to virtual hosts in the `/etc/httpd/conf/httpd.conf` file is shown in the following code:

```
### Section 3: Virtual Hosts
#
# VirtualHost: If you want to maintain multiple domains/hostnames on
# your machine you can setup VirtualHost containers for them. Most
# configurations use only name-based virtual hosts so the server
# doesn't need to worry about IP addresses. This is indicated by the
# asterisks in the directives below.
#
# Please see the documentation at
# <URL:http://httpd.apache.org/docs-2.0/vhosts/>
# for further details before you try to setup virtual hosts.
#
# You may use the command line option '-S' to verify your virtual host
# configuration.
#
# Use name-based virtual hosting.
#
#NameVirtualHost *
#
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
#
# <VirtualHost *> 
#    ServerAdmin webmaster@dummy-host.example.com
#    DocumentRoot /www/docs/dummy-host.example.com
#    ServerName dummy-host.example.com
#    ErrorLog  logs/dummy-host.example.com-error_log
#    CustomLog logs/dummy-host.example.com-access_log common
# </VirtualHost>
```

The following is an example of virtual host directives that would allow you to host the domains handsonhistory.com and linuxtoys.net on the same computer:

```
NameVirtualHost *

<VirtualHost *> 
    DocumentRoot /var/www/handsonhistory
    ServerName www.handsonhistory.com
    ServerAdmin webmaster@handsonhistory.com
    ErrorLog  logs/handsonhistory.com-error_log
    CustomLog logs/handsonhistory.com-access_log common
</VirtualHost>

<VirtualHost *> 
    DocumentRoot /var/www/linuxtoys
    ServerName www.linuxtoys.net
    ServerAdmin webmaster@linuxtoys.net
    ErrorLog  logs/linuxtoys.net-error_log
    CustomLog logs/linuxtoys.net-access_log common
</VirtualHost>
```

### Configuring modules (/etc/httpd/conf.d/*.conf)

Any module that requires special configuration will typically have a configuration file (.conf file) in the /etc/httpd/conf.d directory. Here are module configuration files that are contained in that directory, along with some ways of using those files:

- **auth_mysql.conf** — Configure authentication based on data you add to a MySQL database. Comments in the file describe how to set up the database and how you use it to do user or group authentication before allowing a client to access your Web content.
- **auth_pgsql.conf** — Configure authentication based on data in a PostgreSQL database.
- **htdig.conf** — Identify the location of the htdig search content that can be used on your Web site (/usr/share/htdig is the default location). To see the htdig search screen from a Web browser, type **http://localhost/htdig**.
- **mailman.conf** — Set up mailman list server software so that mailing-list archives can be available from Apache.
