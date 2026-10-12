```
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