Summary 373

```
ud::once:/sbin/update
```

```
ca::ctrllaltdel:/sbin/shutdown -t3 -r now
```

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure
System Shutting Down"
```

```
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored;
Shutdown Cancelled"
```

```
1:2345:respawn:/sbin/minetty tty1
2:2345:respawn:/sbin/minetty tty2
3:2345:respawn:/sbin/minetty tty3
4:2345:respawn:/sbin/minetty tty4
5:2345:respawn:/sbin/minetty tty5
6:2345:respawn:/sbin/minetty tty6
```

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

If you change the contents of /etc/inabb, you must instruct the init process to reread the file. To do so, issue the command

```
init q
```

# Summary

In this chapter, you learned about configuration files and scripts. The most important topics covered are:

The /etc/sysconfig Directory The /etc/sysconfig directory contains a variety of files that hold configuration information, including configuration information for Advanced Power Management (APM), PCMCIA cards, plug-and-play cards, and sound. The network-scripts subdirectory contains scripts used to start up, shut down, and configure networking.

The ifcfg-* Scripts The ifcfg-* scripts store network interface information.