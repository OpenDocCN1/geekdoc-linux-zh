```
``` 
# handle known problems with browser implementations.
# 
BrowserMatch "Mozilla/2" nokeepalive 
BrowserMatch "MSIE 4\\.0b2"  nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\\.0" force-response-1.0
BrowserMatch "Java/1\\.0" force-response-1.0
BrowserMatch "jdk/1\\.0" force-response-1.0
 
#
# The following directive disables redirects on non-GET requests for 
# a directory that does not include the trailing slash.  This fixes a 
# problem with Microsoft WebFolders which does not appropriately handle 
# redirects for folders with DAV methods.
# Same deal with Apple's DAV filesystem and Gnome VFS support for DAV.
 
BrowserMatch "Microsoft Data Access Internet Publishing Provider" 
           redirect-carefully 
BrowserMatch "WebDrive" redirect-carefully 
BrowserMatch "WebDAVFS/1\.0[12]" redirect-carefully
BrowserMatch "gnome-vfs" redirect-carefully
```
```

The BrowserMatch directive enables you to set environment variables based on the contents of the User-agent: header field. The force-response-1.0 variable causes a HTTP/1.0 response, indicating that Apache will respond to the browser in basic HTTP 1.0 operations.

> **NOTE:** If you are following the httpd.conf file, you notice that we are skipping descriptions of the server-status lines and server-info lines. They are described in the “Monitoring Server Activities” section later in this chapter.

# ### Enabling proxy and caching services

Proxy and caching services are turned off by default. You can turn them on by uncommenting the following directives:

```
``` 
# Proxy Server directives. Uncomment the following lines to
# enable the proxy server:

#<IfModule mod_proxy.c> 
#     ProxyRequests On 
#
#<Proxy:*> 
#    Order deny,allow 
#    Deny from all 
#    Allow from .example.com 
#</Proxy>
#
```
```