# Chapter 1. Boot Process, Init, Shutdown

+   - 5 Full multi-user graphical mode (with an X-based login screen)
- 6 Reboot

In general, users operate Red Hat Linux at runlevel 3 or runlevel 5 — both full multi-user modes. Users sometimes customize runlevel 2 and 4 to specific needs. They are not used.
The\ in /etc/inittab. To find the default runlevel for a system, look for the line similar to the one below the top of /etc/inittab:

```
id:5:initdefault:
```

The default runlevel listed in the example above is, as the number after the first colon indicates. To change it, edit /etc/inittab as root.

> Warning
Be careful when editing /etc/inittab. Simple typos can cause the system to become unbootable. If this happens, use a boot diskette, enter single-user mode, or enter rescue mode to boot the computer and repair the file.
For more information on single-user and rescue mode, see the chapter titled Rescue Mode in the Red Hat Linux Customization Guide.

It is possible to change the default runlevel at boot-time by modifying the arguments passed by the boot loader. For information on changing the runlevel at boot time, see Section 2.10 Changing Rules at Boot Time.

# 1.4.2. Runlevel Utilities

One of the best ways to configure runlevels is to use an initscript utility. These tools are designed to simplify the task of maintaining files in the SysV init directory hierarchy and relieves system administrators from having to directly manipulate the numerous symbolic links in the subdirectories of /etc/rc.d/.
Red Hat provides three utilities:

+   - /sbin/chkconfig — The /sbin/chkconfig utility is a simple command-line tool for maintaining the /etc/rc.d/init.d directory hierarchy.
- /sbin/nntys — The curses-based /sbin/nntys utility provides an interactive text-based interface, which some find easier to use than chkconfig.
- Services Configuration Tool — The graphical Services Configuration Tool (redhat-config-services) program is a flexible GTK-based utility for configuring runlevels.

Please refer to the chapter titled Controlling Access to Services in Red Hat Linux Customization Guide for more information regarding these tools.

# 1.5. Shutting Down

To shut down Red Hat Linux, the root user may issue the /sbin/shutdown command. The shut-down page has a complete list of options, but the two most common use are: