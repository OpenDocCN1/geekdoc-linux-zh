# Chapter 21: Setting Up a Web Server

Setting responses to browsers

If extensions are not enough to determine a file's MIME type, you can define hints with the MIMEMagicFile directive. With the BrowserMatch directive, you can set responses to conditions based on particular browser types:

```
#
# The following directives modify normal HTTP response behavior to
# handle known problems with browser implementations.

BrowserMatch "Mozilla/2" keepalive
BrowserMatch "MSIE 4.0;Ob2" keepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4.0" force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "JDK/1.0" force-response-1.0

# The following directive disables redirects on non-GET requests for
# a directory that does not include the trailing slash. This fixes a
# problem with Microsoft WebFolders which does not appropriately handle
# redirects for folders with DAV methods.
# Same deal with Apple's DAV filesystem and Gnome VFS support for DAV.

BrowserMatch "Microsoft Data Access Internet Publishing Provider"
redirect-carefully
BrowserMatch "MS FrontPage" redirect-carefully
BrowserMatch "Webdrive" redirect-carefully
BrowserMatch "WebDAVs/1.0 [0123]" redirect-carefully
BrowserMatch "gnome-vfs/1.0" redirect-carefully
BrowserMatch "XML Spy" redirect-carefully
BrowserMatch "Dreamweaver-WebDAV-SCM1" redirect-carefully
```

The BrowserMatch directive enables you to set environment variables based on the User-agent: header field. The force-response-1.0 causes a header indicating that Apache will respond to the browser in basic HTTP 1.0 operations.

> NOTE: If you are following the httpd.conf file, we notice that we are skipping descriptions of the server-status and server-info files. They are described in the section "Monitoring Server Activities" later in this chapter.

# Enabling proxy and caching services

Proxy and caching services are turned off by default. You can turn them on by uncommenting the following directives: