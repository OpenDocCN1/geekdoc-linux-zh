```
# The following directive disables redirects on non-GET requests for
#	a directory that does not include the trailing slash.  This fixes a
#	problem with Microsoft WebFolders which does not appropriately handle
#	redirects for folders with DAV methods.
#	Same deal with Apple's DAV fileSystem and Gnome VFS support for DAV.
#
BrowserMatch "Microsooft\s+Data\s+Access\s+Internet\s+Publishing\s+Provider"
	"redirect-carefully"
BrowserMatch "MS FrontPage" redirect-carefully
BrowserMatch "*WebDrive" redirect-carefully
BrowserMatch "*WebDAVS/1.\[0123\]" redirect-carefully
BrowserMatch "*gnome-vfs/1.0*" redirect-carefully
BrowserMatch "*XML Spy*" redirect-carefully
BrowserMatch "*Dreamweaver-WebDAV-SCM1*" redirect-carefully
```

The **BrowserMatch** directive enables you to set environment variables based on the contents of the **User-Agent** header field. The **force-response-1.0** variable causes a HTTP/1.0 response, indicating that Apache will respond to the browser in basic HTTP 1.0 operations.

> **NOTE** If you are following the httpd.conf file, you notice that we are skipping descriptions of the server-status lines and server-info lines. They are described in the section “Monitoring Server Activities” later in this chapter.

# Enabling Proxy and Caching Services

Proxy and caching services are turned off by default. You can turn them on by uncommenting the following directives:

```
#
#	Proxy Server directives. Uncomment the following lines to
#	enable the proxy server:
#
#<IfModule mod_proxy.c>
#	ProxyRequests On
#
#<Proxy:*
#		Order deny,allow
#		Deny from all
#		Allow from .example.com
#</Proxy>
#
#	Enable/disable the handling of HTTP/1.1 “Via:” headers.
#	(“Full” adds server version; “Block” removes outgoing Via: headers)
#	Set to one of: Off | On | Full | Block
#
#ProxyVia On
```

# To enable a cache of proxied content, uncomment the following lines.