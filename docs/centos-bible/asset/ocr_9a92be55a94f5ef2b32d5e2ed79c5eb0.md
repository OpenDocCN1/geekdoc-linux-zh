# ### Configuring Caching in squid.conf

Caching, as it relates to a proxy server, is the process of storing data on an intermediate system between the Web Server that sent the data and the client that received it. The assumption is that later requests for the same data can be serviced more quickly by not having to go all the way back to the original server. Instead, the proxy server can simply send you the content from its copy in cache. Another benefit of caching is that it reduces demands on network resources and on the information servers.

You can arrange caching with other caching proxy servers to form a cache hierarchy. The idea is to have a *parent cache* exist close to an entry to the Internet backbone. When a *child cache* requests an object, if the parent doesn't have it, the parent goes out and gets the object, sends a copy to the child, and keeps a copy itself. That way, if another request for that data comes to the parent, it can probably service that request without making another request to the original server. This hierarchy also supports *sibling caches*, which can, in effect, create a pool of caching servers on the same level.

> **CAUTION**
> 
> Caching can consume a lot of your hard disk space if you let it. If you have separate partitions on your system, make sure you have enough space in /var to handle the added load.

Here are some cache-related tags that you should consider setting:

+   cache_peer — If there is a cache parent whose resources you can use, you can add the parent cache using this tag. You would need to obtain the parent cache's hostname, the type of cache (parent), proxy port (probably 3128), and ICP port (probably 3130) from the administrator of the parent cache. If you have no parent cache, you don't have to set this value. Here's an example of a cache_peer entry:
+   
+   cache_peer parent.handsonhistory.com parent 3128 3130
+   
+   You can also add options to the end of the line, such as *proxy-only*, so that what you get from the parent isn't stored locally, and *weight=n* (where *n* is replaced by a number above 1 to indicate that the parent should be used above other parents). Add *default* if the parent is used as a last resort when all other parents don't have the requested data.

+   cache_mem — Specifies the amount of cache memory (RAM) used to store in-transit objects (ones that are currently being used), hot objects (ones that are used often), and negative-cached objects (recent failed requests). The default is 8 MB, although you can raise that value. To set *cache_mem* to 16 MB, enter the following:
+   
+   cache_mem    16 MB

> **NOTE**
> 
> Because *Squid* will probably use a total of three times the amount of space you give it for all its processing, *Squid documentation* recommends that you use a *cache_mem* size one-third the size of the space that you actually have available for *Squid*.

+   cache_dir — Specifies the directory (or directories if you want to distribute the cache across multiple disks or partitions) in which cache swap files are stored. The default is