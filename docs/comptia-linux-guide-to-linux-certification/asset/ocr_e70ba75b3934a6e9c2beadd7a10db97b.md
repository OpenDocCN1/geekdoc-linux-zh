![](bbox=[0.15, 0.09, 0.6, 0.37])

On Linux systems that use the upstart init system, the `/etc/rc[runlevel].d` directories are not used. Instead, the init daemon identifies the default runlevel in the `/etc/inittab` file and then directly executes the rc scripts within the `/etc/init.d` directory to start or stop the appropriate daemons based on the information specified in the configuration files within the `/etc/init` directory. Each daemon has a separate configuration file within the `/etc/init` directory that uses standard wildcard notation to identify the runlevels in which it should be started or stopped. For example, the `/etc/init/cron.conf` file shown next indicates that the cron daemon should be started in runlevels 2, 3, 4, and 5 ([2345]) and not be stopped in runlevels 2, 3, 4, and 5 ([12345]):

```
[root@server1 ~]# cat /etc/init/cron.conf
# cron - regular background program processing daemon
#
# cron is a standard UNIX program that runs user-specified programs at
# periodic scheduled times
description     "regular backgrouond program processing daemon"
start on runlevel [2345]
stop on runlevel [12345]

expect fork
respawn

exec cron
[root@server1 ~]# _
```

Figure 8-6 illustrates the upstart system initialization process for a system that boots to run-level 5.

![](bbox=[0.15, 0.87, 0.35, 0.94])

Some daemons are not compatible with the upstart init system. As a result, Linux distributions that use the upstart init system often host several traditional UNIX SysV daemons that are started via entries in the `/etc/rc[runlevel].d` directories.