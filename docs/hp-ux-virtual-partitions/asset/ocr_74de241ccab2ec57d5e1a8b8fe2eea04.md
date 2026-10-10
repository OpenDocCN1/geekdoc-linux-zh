can be used to cold-install HP-UX over an existing instance.

ignite_kernel can reside either on the current virtual partition (the one on which vpboot is run) or on any other networked system or virtual partition accessible from that partition. The syntax for ignite_kernel is:

```
[Server name or IP addr,]cold-install_kernel
```

If cold-install_kernel begins with a slash, “/”, you are specifying an absolute path and vpboot looks for it at that location. If cold-install_kernel does not begin with “/”, the default path /opt/ignite/boot/ is prepended to cold-install_kernel.

If the Server name or IP address is not specified, vpboot loads the cold-install kernel from the filespace of the current virtual partition. Otherwise the command loads it from the filespace of the specified server. The comma is a required part of the server name syntax.

# RETURN VALUE

The vpboot command exits with one of the following values:

+   *   0 Successful completion.
+   *   1 One or more error conditions occurred.

# EXAMPLES

Boot the virtual partition called Oslo

```
vpboot -p Oslo
```

Boot the virtual partition Bergen specifying an alternate kernel

```
vpboot -p Bergen -b /stand/vmunix_debug
```

Cold-install the virtual partition Trondheim from a file on a remote server

```
vpboot -p Trondheim -i mysys.myserver.mysdomain.com:/mypath/mysinst
```

Cold-install the virtual partition Sandefjord from a file at the default path /opt/ignite/boot on the current virtual partition

```
vpboot -p Sandefjord -I MINSTALL
```

# ERRORS

vpboot displays error messages on stderr for any of the following conditions:

VP_name does not exist in the monitor.

VP_name is in some state other than Down, and so cannot be booted. Use the vpareset(1M) command instead.