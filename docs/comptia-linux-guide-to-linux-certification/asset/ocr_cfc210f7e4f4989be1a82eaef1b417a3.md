Alternatively, you can specify to start the postfix daemon only in runlevels 2 and 5 using the following command that creates the rc scripts using a sequence number of 20:

```
[root@server1 ~]# update-rc.d postfix start 20 2 5 S stop 20 0 1 3 4 6 .
update-rc.d: warning: start runlevel arguments (5) do not match postfix
Default-Start values (2 3 4 5)
update-rc.d: warning: stop runlevel arguments (1 2 3 4 6) do not match post-
fix Default-Stop values (0 1 6)
Adding system startup for /etc/init.d/postfix ...
/etc/rc1.d/K00postfix -> ../init.d/postfix
/etc/rc3.d/K00postfix -> ../init.d/postfix
/etc/rc4.d/K00postfix -> ../init.d/postfix
/etc/rc6.d/K00postfix -> ../init.d/postfix
/etc/rc2.d/S20postfix -> ../init.d/postfix
/etc/rc5.d/S20postfix -> ../init.d/postfix
[root@server1 ~]#_
```

# Working with the Systemd System Initialization Process

Like the UNIX SysV init daemon, the Systemd init daemon is used to start daemons during system initialization as well as start and stop daemons after system initialization. However, Systemd can also be used to start, stop, and configure many other operating system components. To Systemd, each operating system component is called a unit. Daemons are called *service units* because they provide a system service, and runlevels are called *target units* (or targets). By default, each target maps to a UNIX SysV runlevel:

+   * `poweroff.target` is the same as Runlevel 0.
+   * `rescue.target` is the same as Runlevel 1 (Single User Mode).
+   * `multi-user.target` is the same as Runlevel 2, 3 and 4.
+   * `graphical.target` is the same as Runlevel 5.
+   * `reboot.target` is the same as Runlevel 6.

![](bbox=[0.14, 0.69, 0.44, 0.81])

> The `graphical.target` first loads all daemons from the `multi-user.target`.

The default target on a system that has a GUI environment installed is the `graphical.target`. To configure your system to instead boot to the `multi-user.target`, you can update the `/etc/systemd/system/default.target` symbolic link to point to the correct runlevel using the following command:

```
[root@server1 ~]# ln -s /lib/systemd/system/runlevel3.target /etc/
systemd/system/default.target
[root@server1 ~]#_
```

Most of the rc scripts that are used by Systemd to start and stop daemons are stored in the `/usr/lib/systemd/system` directory and called `[daemon].service`. For example, the script for the cron daemon is `/usr/lib/systemd/system/crond.service`. To ensure that the cron daemon is...