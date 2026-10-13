The following example uses the **cachefsstat** command to display the cached file system statistics:

```
```shell
# cachefsstat /home

    /home

              cache hit rate:    57% (8 hits, 6 misses)
              consistency check: 14 (14 pass, 0 fail)
                      modifies:   0
               garbage collection: 0

#
```
```

![](bbox=[0.123, 0.277, 0.219, 0.341])

> > Note that the **cfsadmin -l** command reports on the configuration status (tunable parameters) of the cache, whereas the **cachefsstat** reports on the contents of the cache (cached file system statistics).

# Checking the Consistency of a Cache

To be certain that information in a cache is up to date, periodic consistency checks are performed automatically. These checks could increase network activity, however. To reduce the amount of network traffic, you can disable the automatic consistency checking and check the consistency manually (on demand).

To disable automatic consistency checking (that is, to request on-demand consistency checking), specify the **demandconst** option when the file system is mounted. The line is wrapped to improve readability:

```
```shell
# mount -F cachefs -o backfstype=nfs,cachedir=/cache,demandconst
sparc20:/export/home /home
#
```
```

To perform a consistency check on demand, use **cfsadmin -s** followed by a mount point of the cached file system as a command-line argument:

```
```shell
# cfsadmin -s /home
#
```
```

# Managing a Cache Log

The **cachefslog**(1M) command is used to set up, verify, and halt CacheFS logging. The **cachefsswsize**(1M) command is used to analyze the log to determine a recommended working set size for the cache. A cache that’s too small causes access delays and higher network traffic (a low cache hit rate). A cache that’s too large wastes file system space.