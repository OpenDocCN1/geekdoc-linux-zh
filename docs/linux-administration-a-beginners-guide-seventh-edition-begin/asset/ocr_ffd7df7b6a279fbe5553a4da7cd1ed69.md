# Shutting Down Non-xinetd Services

If a service is not managed by xinetd, then a separate process or script that is started at boot time is running. If the service in question was installed by your distribution, and your distribution offers a nice tool for disabling a service, you may find that to be the easiest approach.

For example, some Linux distros support the chkconfig program, which provides an easy way to enable and disable individual services. For example, to disable the rpcbind service from starting in runlevels 3 and 5 on such systems, employ the following:

```
[root@server ~]# chkconfig --level 35 rpcbind off
```

The parameter --level refers to the runlevels that should be affected by the change. Since runlevels 3 and 5 represent the two multiuser modes, we select those. The rpcbind parameter is the name of the service referred to in the /etc/init.d/ directory. Finally, the last parameter can be set to on, off, or reset. The on and off options are self-explanatory. The reset option refers to resetting the service to its native state at.

If you want to turn the rpcbind service on again, simply run the:

```
[root@server ~]# chkconfig --level 35 rpcbind on
```

Note that chkconfig doesn't actually turn an already running service on or off; instead, it defines what will happen at the next startup time. To stop the process, use the control script in the /etc/init.d/ directory. In the case of rpcbind, you would stop it with:

```
[root@server ~]# /etc/init.d/rpcbind stop
```

On Linux distributions running systemd (such as Fedora), you can alternatively stop a service using the systemctl command. For example, to stop the rpcbind service, type the:

```
[root@fedora-server ~]# systemctl stop rpcbind.service
```

Similarly, to permanently disable the rpcbind unit from starting up the next system boot, use the systemctl utility, type

```
[root@fedora-server ~]# systemctl disable rpcbind.service
```

# Monitoring Your System

Free and open source commercial-grade applications that perform monitoring and are well worth checking out. Here, we'll take a look at a variety of excellent tools that help with system monitoring. Some of these tools already installed with your Linux distributions; others don't. All are free and easily acquired.