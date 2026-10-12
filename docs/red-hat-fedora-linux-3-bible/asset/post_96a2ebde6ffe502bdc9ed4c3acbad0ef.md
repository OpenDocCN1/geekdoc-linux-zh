
## Adding MIME types and handlers

With the AddType directive, you can enhance the MIME types assigned for your Apache Web server without editing the /etc/mime.types file. With the AddHandler directive, you can map selected file extensions to handlers (that result in certain actions being taken):

```
# AddType allows you to add to or override the MIME configuration
# file mime.types for specific file types.

AddType application/x-tar.tgz

#

# For server-parsed imagemap files:

AddHandler imap-file map

# For type maps (negotiated resources):
# (This is enabled by default to allow the Apache "It Worked" page
# to be distributed in multiple languages.)

AddHandler type-map var
```

## Defining actions and headers

Some types of media can be set to execute a script when they are opened. Likewise, certain handler names, when opened, can be set to perform specified scripts. The Action directive can be used to configure these scripts:

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location
```

The Action directive maps a CGI script to a handler or a MIME type, whereas the Script directive maps a CGI script to a particular HTTP request method (GET, POST, PUT, or DELETE). These options allow scripts to be executed whenever a file of the appropriate MIME type is requested, a handler is called, or a request method is invoked.

## Customizing error responses

For different error conditions that occur, you can define specific responses. The responses can be in plain text, redirects to pages on the local server, or redirects to external pages:

```
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 /cgi-bin/missing_handler.pl
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

As the comments suggest, the `ErrorDocument` directive can customize any server response code, redirecting it to an external page, a local file or CGI script, or to a simple text sentence. Table 21-6 lists the most common server response codes and their meanings.

### Table 21-6: HTTP Response Codes

| Response Code | Meaning |
| :--- | :--- |
| 200 OK | The request was successfully processed. |
| 201 Created | Using the POST request method, a new file was successfully stored on the server. |
| 202 Accepted | The request has been received and is currently being processed. |
| 204 No Content | The request was successful, but there is no change in the current page displayed to the client. |
| 301 Moved Permanently | The requested page has been permanently moved, and future references to that page should use the new URL that is displayed. |
| 302 Moved Temporarily | The requested page has been temporarily relocated. Future references should continue to use the same URL, but the current connection is being redirected. |
| 304 Not Modified | A cached version of the page is identical to the requested page. |
| 400 Bad Request | The client's request contains invalid syntax. |
| 401 Unauthorized | The client specified an invalid user/password combination. |
| 402 Payment Required | The client must provide a means to complete a monetary transaction. |
| 403 Forbidden | Access-control mechanisms deny the client's request. |
| 404 Not Found | The requested page does not exist on the server. |
| 500 Internal Server Error | Usually encountered when running a CGI program, this response code indicates that the program or script contains invalid code or was given input that it cannot handle. |
| 501 Not Implemented | The request method (for example, GET, POST, PUT, DELETE, HEAD) is not understood by the server. |
| 502 Bad Gateway | Using the Web server as a proxy, an error was encountered in fulfilling the request to an external host. |
| 503 Service Unavailable | The server is currently processing too many requests. |
| 505 HTTP Version Not Supported | The request version (for example, HTTP/1.0, HTTP/1.1) is not understood by the server. |

To make it easier to internationalize error messages and standardize how these messages are presented, the latest version of Apache includes what are referred to as variant pages (ending in a .var suffix). These variant pages, which offer variable output based on language, are stored in the /var/www/error directory.

```
Alias /error/ "/var/www/error/"
<IfModule mod_negotiation.c>
<IfModule mod_include.c>
<Directory "/var/www/error">
AllowOverride None
Options IncludesNoExec
AddOutputFilter Includes html
AddHandler type-map var
Order allow,deny
Allow from all
LanguagePriority en es de fr
ForceLanguagePriority Prefer Fallback
</Directory>

ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html.var
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html.var
```

The ErrorDocument directive associates a particular error code number with a particular .var file that contains multiple possible responses based on language.

## Setting responses to browsers

If file extensions are not enough to determine a file’s MIME type, you can define hints with the MimeTypeMagicFile directive. With the BrowserMatch directive, you can set responses to conditions based on particular browser types:

```
#
# The following directives modify normal HTTP response behavior to
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

The BrowserMatch directive enables you to set environment variables based on the contents of the User-agent: header field. The force-response-1.0 variable causes a HTTP/1.0 response, indicating that Apache will respond to the browser in basic HTTP 1.0 operations.

> **NOTE:** If you are following the httpd.conf file, you notice that we are skipping descriptions of the server-status lines and server-info lines. They are described in the “Monitoring Server Activities” section later in this chapter.

## Enabling proxy and caching services

Proxy and caching services are turned off by default. You can turn them on by uncommenting the following directives:

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
# Enable/disable the handling of HTTP/1.1 "Via:" headers.
# ("Full" adds server version; "Block" removes outgoing Via: headers)
# Set to one of: Off | On | Full | Block
#
#ProxyVia On

# To enable a cache of proxied content, uncomment the following lines.
# See http://httpd.apache.org/docs-2.0/mod/mod_cache.html for more details.
#
#<IfModule mod_disk_cache.c>
# CacheEnable disk /
# CacheRoot "/var/cache/mod_proxy"
#</IfModule>

#</IfModule>
# End of proxy directives.
```

Apache can function as a proxy server, a caching server, or a combination of the two. If `ProxyRequests` is set to *Off*, the server will simply cache files without acting as a proxy. If `CacheRoot` (which specifies the directory used to contain the cache files) is undefined, no caching will be performed. Both proxy and caching services are *Off* (commented out) by default.

If you turn on caching, the `CacheRoot` should exist on a file system with enough free space to accommodate the cache, which is limited by the `CacheSize` directive. However, you should have 20 to 40 percent more space available in the file system because cache cleanup (to maintain the `CacheSize`, in kilobytes) occurs only periodically (which you can set using the `CacheGcInterval` directive).

You can add other directives to this example to enable other caching features. The `CacheMaxExpire` directive can indicate the maximum number of hours that a document will exist in the cache without checking the original document for modifications. The `CacheLastModifiedFactor` applies to documents that do not have an expiration time, even though the protocol would support one. To formulate an expiration date, the factor (a floating-point number) is multiplied by the number of hours since the document’s last modification. For example, if the document was modified three days ago and the `CacheLastModifiedFactor` were 0.25, the document would expire from the cache in 18 hours (as long as this value is still below the value of `CacheMaxExpire`).

The `CacheDefaultExpire` directive (specifying the number of hours before a document expires) applies to documents received via protocols that do not support expiration times. The `NoCache` directive contains a space-separated list of IP addresses, host names, or keywords in host names that should not have documents cached.

Here’s how the caching server behaves if you uncomment the previous `Cache` lines:
