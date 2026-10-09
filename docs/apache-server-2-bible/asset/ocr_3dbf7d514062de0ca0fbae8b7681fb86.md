including Linux, is threaded instead of `perchild`, the `if` condition will be true and Apache will set the `ScoreBoardFile` directive. This directive is used to point to a file, which is used to exchange run-time status information between Apache processes. If you have a RAM disk, you might consider putting this file in the RAM disk to increase performance a bit. In most cases, you should leave this directive alone.

# **Timeout, KeepAlive, MaxKeepAliveRequests, and KeepAliveTimeout**

`Timeout` sets the server timeout in seconds. The default should be left alone. The next three directives `KeepAlive`, `MaxKeepAliveRequests`, and `KeepAliveTimeout` are used to control the keep-alive behavior of the server. You do not need to change them.

# **IfModule containers**

Apache will use one of the next three `<IfModule ...>` containers based on which MPM you chose. For example, if you configured Apache using the default MPM mode (threaded) on a Linux system, then the following `<IfModule ...>` container will be used:

```
```
<IfModule threaded.c>
    StartServers      3
    MaxClients        8
    MinSpareThreads   5
    MaxSpareThreads  10
    ThreadsPerChild  25
    MaxRequestsPerChild 0
</IfModule>
```
```

On the other hand, if you chose `--with-mpm=prefork` during source configuration by using the configure script, then the following `<IfModule ...>` container will be used:

```
```
<IfModule prefork.c>
    StartServers      5
    MinSpareServers  15
    MaxSpareServers  10
    MaxClients       20
    MaxRequestsPerChild 0
</IfModule>
```
```

Similarly, the `--with-mpm=perchild` option forces Apache to use the last `<IfModule ...>` container.

# **Directives for threaded (default) MPM behavior**

If you followed my advice in the previous chapter, you did not change the default MPM behavior during source compilation and used the threaded behavior, so the directives that you need to consider are discussed below.