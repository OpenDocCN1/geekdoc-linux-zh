# Configuring caching in squid.conf

Caching, it relates to a proxy server, is the process of storing data on an intermediate system between the Web server that sent the data and the client that received it. The assumption is that later requests for the same data can be served more quickly by not having to go all the way back to the original server. Instead, the proxy server can simply send the content from its copy. Another benefit of caching is that it reduces demand on network resources and on information servers.

You can arrange caching with other proxy servers to form a cache hierarchy. The idea is to have a parent cache exist close to the Internet backbone. When a child cache requests an object, if the parent doesn't have it, the parent goes out and gets the object, sends a copy to the child, and keeps a copy itself. If another request for the data comes to the parent, it can probably serve without making another request to the original server. This hierarchy also supports siblings caches, which can, in effect, create a pool of caching servers on the same level.

> CAUTION: Caching can consume some of your hard disk space if you let it. If you have separate partitions on your system, make sure that you have enough space in /var to handle the added load.

Here are some cache-related tags that you should consider:

+   - cache_peer — If there is a cache parent whose resource you use, you can add the parent cache using this. You would need to indent the parent cache's hostname, the type of cache (parent), proxy port (probably 3128) and ICP port (probably 3130) from the administrator of the parent cache. (If you have no parent cache, you don't have to set this value.) Here's an example of a cache_peer entry:
```
cache_peer parent.handhistory.com parent 3128 3130
```

You can also add options to the end of the line, such as proxy-only (so that what you get from the parent isn't stored locally) and weight=n (where n is replaced by a number 1 to indicate that the parent should be used over other parents). Default if the parent is used as a last resort (when all other parents don't have the requested data).

+   - cache_mem — Specifies the amount of cache memory (RAM) used to store in-transit objects (that are currently being used), objects (that are used often), and negative-cached objects (failed requests). The default is 8MB, you can increase that value. To cache_mem to 16MB, enter the following:
```
cache_mem 16 MB
```

> NOTE: Because Squid will probably use a total of three times the amount of space you give it for all its processing, Squid recommends that you use a cache_mem size one-third of the space that you actually have available for Squid.