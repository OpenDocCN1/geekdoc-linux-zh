12. The route command lists the current routing table of the local system. Other acceptable answers include route -n, netstat -r, and netstat -rn.

# Time Synchronization

13. The system-config-date command starts the Date/Time Configuration tool.

# LAB ANSWERS

Yes, there are many Linux systems that run for years at a time without a reboot. But reboots are sometimes required, such as when newer kernels are installed. So when configuring a Linux system, make sure any changes survive a reboot. Otherwise, your supervisor may not believe that you ever did the work. On a Red Hat exam, you won't get credit unless changes survive a reboot.

# Lab 1

If successful, this lab will show you how to change the default runlevel, along with the relative importance of the options in the GRUB bootloader. Normally, it's best to back up a file before making changes. However, the RHEL 6 version of the /etc/inittab file is pretty simple, as it contains only one line of significance:

```
id:5:initdefault:
```

This assumes the default runlevel is 5; if there's a different default runlevel for your system, substitute accordingly.

# Lab 2

This lab should make a point: it's far too easy in the default configuration of RHEL 6 to get access to the root administrative account.

If you had to back up the /etc/shadow file and were successful with this lab, you should not have to restore that file from backup. The passwd commands executed during this lab should have restored the intended password for the root administrative user. One way to meet the requirements of this lab is with the following steps:

+   1. Power up the local system. During the boot process, when you see the following message (the operating system name and version number may vary), press a key.

```
Booting Red Hat Enterprise Linux Server (2.6.32-71.el6.x86_64) in 5 seconds....
```