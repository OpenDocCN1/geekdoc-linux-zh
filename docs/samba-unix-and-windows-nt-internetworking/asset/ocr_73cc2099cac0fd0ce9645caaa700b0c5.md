System sluggishness related to IO can be monitored using the UNIX iostat command. Use the -d option to display disk IO activity. For each disk, statistics include the number of transfers per second, bytes transferred per second and milliseconds per average seek. Note that not all drive types will report seek times. You can also specify a time interval and count for recording activity snapshots over time.

```
# iostat -d [drive ...] [interval] [count]
```

Take a close look at Samba locking options. For shares that require locking, it is a good idea to make sure that opportunistic locking (oplock) parameters are enabled. oplocks allow clients to use aggressive caching and can achieve performance improvements over standard locking by as much as 30%. Also consider disabling strict locking. When enabled, strict locking directs the server to check lock status on every file access.

The majority of network tuning should be handled at the OS level. Samba does provide a socket option parameter for adjusting tcp and socket settings like buffer size and keep alive time (Table 15.5). The tcp_nodelay value is the only one enabled by default. Any value adjustments made with these parameters need to fit corresponding OS level settings.

```
socket option = <value list>
```

```
socket option = tcp_nodelay so_reuseaddr
```

# Table 15.5 Samba Socket Option Values

+   - so_keepalive
+   - so_reuseaddr
+   - so_broadcast
+   - tcp_nodelay
+   - iptos_lowdelay
+   - iptos_throughput
+   - so_sndbuf=<integer>
+   - so_rcvbuf=<integer>
+   - so_sndlowat=<integer>
+   - so_rcvlowat=<integer>

# Logging

It is always nice to have help when debugging a problem. One of the best ways to get help is by setting verbose logging and diagnostic options. You'll need to make tradeoffs between performance hits due to generous logging activity and the problem state. Turn diagnostics up during incident sleuthing and down during normal operation.

Log file and general diagnostic behavior is determined by the log file, max log size, and debug level parameters. Log files normally reside in the /usr/local/samba/var directory. By using substitution variables in the log file name, it is possible to generate logs by user, client NetBIOS name, or architecture. By default both smbd and nmbd generate logs named log.smb and log.nmb. The max log size