server. (If your system runs `inetd`, you may want to read both the `inetd` and `xinetd` sections, because `xinetd` configuration is rather like an expanded version of `inetd` configuration.) The final part of this task is to test your configuration to be sure it's working correctly.

# ## Identifying Your Super Server

Linux distributions have traditionally used `inetd`, but they've been slowly shifting to `xinetd`. Both super servers offer similar basic features, but `xinetd` provides *more* features, particularly in the area of access control options. Using `xinetd`, you can restrict who may access a server based on IP address, network port, time of day, and more. You can use a package called TCP Wrappers in conjunction with `inetd` to provide similar access controls. An additional advantage of `xinetd` is that its configuration file can be split into parts. This enables distributions that use `xinetd` to provide `xinetd` configuration files with individual servers, simplifying configuration.

Type `ps ax | grep inetd` to see which super server is running on your system—the output should include a line with either the `inetd` or the `xinetd` command. Some systems run neither super server, though. If you can't find a trace of either server, use your package manager to search for the `inetd` and `xinetd` packages. If one is installed, you might need to modify your SysV configuration to launch the server in your runlevel, as described in Phase 3. If neither package is installed, install one (preferably `xinetd`) using your distribution's package management tools, as described in Phase 3.

# ## Configuring `inetd`

You control servers that launch via `inetd` through the `/etc/inetd.conf` file. This file consists of a series of lines, one for each server. A typical line resembles the following:

```
```text
ftp stream tcp nowait root /usr/sbin/tcpd /usr/sbin/ftpd -l
```
```

![](bbox=[0.15, 0.64, 0.25, 0.7])

If your system doesn't use `ftpd`, or if it's called `in.ftpd` or is located in a directory other than `/usr/sbin`, adjust the command appropriately. The `-l` option is specific to `ftpd` and so may also need to be changed for your FTP server.

Each line consists of several fields separated by one or more spaces. The meanings of these fields are as follows:

**Service name** The first field (`ftp` in the preceding example) is the name of the service as it appears in the `/etc/services` file.

**Socket type** The socket type entry tells the system what type of connection to expect—a reliable two-way connection (`stream`), a less-reliable connection with less overhead (`dgram`), a low-level connection to the network (`raw`), or various others. The differences between these types are highly technical; your main concern in editing this entry should be to correctly type the value specified by the server's documentation.

**Protocol** This is the TCP/IP Transport-layer protocol used, usually `tcp` or `udp`.