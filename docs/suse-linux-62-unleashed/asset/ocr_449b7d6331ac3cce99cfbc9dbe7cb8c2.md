# Introduction and Installation SuSE Linux
PART I

+   - Deletes stale subsystem files

+   - Deletes stale pid files

+   - Sets the system clock

+   - Loads modules

That's a lot of work for the first startup script, but it's only the first step in a number of steps needed to start your system. You've seen that the init command is run after the Linux kernel is loaded. After boot is run by init, it runs boot.local.

# When the Runlevel Changes

When the system boots, SuSE Linux will then run /sbin/init.d/rc to start services according to set environment variables or settings in /etc/rc.config. You can also change your system to a new runlevel with the telinit command:

```
# telinit N
```

where N is a runlevel. For example, you can use the following command to shutdown your system:

```
# sbin/init.d
```

The directory contains a pertinent script for each service or action assigned to a runlevel (these scripts are symlinked to /etc/rcX.subdirectories; the runlevel directories are under /sbin/init.d). For example, when a change of runlevel is requested (say to 2), the scripts beginning with S (for start) in the rc2 directory are in alphabetical order. On the other hand, when shutting down or rebooting SuSE Linux (runlevel 0), the scripts beginning with K (for kill) in the rc0 directory are in order.

These listed S or K scripts are symbolic links to the main system initialization scripts:

```
# ls -1/sbin/init.d/rc2.*
```

```
drwxr-xr-x 1 root root  Aug 31 07:17 K20apache -> ../apache
drwxr-xr-x 1 root root  Aug 31 07:00 K20apmd -> ../apmd
drwxr-xr-x 1 root root  Aug 05 06:55 K20at -> ../at
drwxr-xr-x 1 root root  Aug 31 07:19 K20atalk -> ../atalk
...
drwxr-xr-x 1 root root  Oct 10 06:57 S01kernel -> ../kernel
drwxr-xr-x 1 root root  Aug 09 06:57 S02serial -> ../serial
drwxr-xr-x 1 root root  15 Aug 31 07:17 S03i41_hardware -> ../i41
drwxr-xr-x 1 root root  9 Aug 31 06:55 S03pcmcia -> ../pcmcia
```