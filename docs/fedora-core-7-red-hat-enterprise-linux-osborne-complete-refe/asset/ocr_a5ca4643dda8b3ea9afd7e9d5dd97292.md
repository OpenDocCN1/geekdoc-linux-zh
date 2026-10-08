# Memory and Disk Configuration

Squid provides several options for configuring cache memory. The **cache_mem** option sets the memory allocated primarily for objects currently in use (objects in transit). If available, the space can also be use for frequently accessed objects (hot objects) and failed requests (negative-cache objects). The default is 8MB. The following example sets it to 256 MB:

```
```
cache_mem 256 MB
```
```

You can further specify the minimum and maximum sizes of objects saved either on disk or in memory. On disk, you use **maximum_object_size** and **minimum_object_size**. The default maximum is 4 KB. The default minimum is set to 0, indicating no minimum. For memory, you use **maximum_object_size_in_memory** and **minimum_object_size_in_memory**.

The **cache_swap_low** and **cache_swap_low** options let you set bars for replacing objects in your cache.

To designate where cache objects are to be located, you use the **cache_dir** option. Here you specify what directories to use for your cache.

# Administrative Settings

The e-mail address for the administrator for your Squid cache is specified in the **cache_mgr** option.

If you run Squid as the root user, then Squid will change its user and group ID from **root** to **nobody**. The group ID will be changed to **nogroup**. This is to protect root user access. Should you run Squid as a user other than root, Squid will retain that original user as its user ID. If, when running Squid from the root user, you want to designate another user other than **nobody**, you can use **cache_effective_user** to change user IDs, and **cache_effective_group** to change the group.

You can also specify a special host name to be displayed in error messages. Use **visible_hostname** to set the name.

# Logs

Squid keeps several logs detailing access, cache performance, and error messages.

+   - **access.log** holds requests sent to your proxy.

+   - **cache.log** holds Squid server messages such as errors and startup messages.

+   - **store.log** holds information about the Squid cache, such as objects added or removed.

You can use the cache manager (**cachemgr.cgi**) to manage the cache and view statistics on the cache manager as it runs. To run the cache manager, use your browser to execute the **cachemgr.cgi** script (this script should be placed in your Web server's **cgi-bin** directory).

# Web Server Acceleration: Reverse Proxy Cache

Though Squid caches can enhance access by clients to a Web server, Squid can also reduce the load on a Web server. Web servers that become overwhelmed by requests can move their cachable pages to a Squid proxy server that can serve as a kind of alternate site,