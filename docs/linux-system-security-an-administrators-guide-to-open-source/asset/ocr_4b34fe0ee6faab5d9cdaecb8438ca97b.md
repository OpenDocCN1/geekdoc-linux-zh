the /etc/rc.d/rcN.d directory, where *N* may be any one of the integers 0 through 9 inclusive. Thus it is these start-up (often referred to as start/stop or start/kill) scripts that define a run level.

You may change run levels by executing init *N*, where *N* is any one of the integers 0 through 9 inclusive, or *s*, or *S*. If the run level is not defined, init simply exits. You may determine the system’s current run level by executing the /sbin/runlevel command.

Additional information about init and runlevel are available in the init(8) and runlevel(8) man pages. For more complete details related to this topic, check out the books

+   1. Hein, Jochen, Linux Companion for System Administrators, Harlow, England, Addison Wesley Longman Limited, 1999.

+   2. Komarski, Mark F., and Cary Collett, Linux System Administrator’s Handbook, Upper Saddle River, New Jersey, Prentice Hall PTR, 1998.

or other similar resources.

We will refer to start-up scripts at various points in this book. Here, we will provide a brief description of the structure, common use, and manipulation of start-up scripts.

By default, all of the start-up scripts except for /etc/rc.d/rc.local are located in the directory /etc/rc.d/init.d. The scripts found in /etc/rc.d/rcN.d directories previously mentioned are symbolic links (refer to the ln(1) man page for information about symbolic links) to the entries in /etc/rc.d/init.d. Each script in /etc/rc.d/init.d may accept a number of arguments, but minimally will accept the two arguments: start and stop. When a script is executed with the start argument, then the process or processes controlled by that script will be started. Given the stop argument, then the process or processes will be terminated.

For example, the script /etc/rc.d/init.d/lpd, which controls the /usr/sbin/lpd daemon, is symbolically linked to by the scripts shown in Example 3-4. The scripts in Example 3-4 are normally only invoked through init. When invoked by init, the scripts whose names begin with *K* will cause /etc/rc.d/init.d/lpd to be invoked with the stop argument and those beginning with *S* will cause /etc/rc.d/init.d/lpd to be invoked with the start argument. The number 60 is used to determine the invocation order with respect to other scripts in the same directory that the lpd script is in.

# **Example 3-4** Symbolic Links to /usr/sbin/lpd

```
"""
/etc/rc.d/rc0.d/K60lpd
/etc/rc.d/rc1.d/K60lpd
/etc/rc.d/rc2.d/S60lpd
/etc/rc.d/rc3.d/S60lpd
/etc/rc.d/rc4.d/S60lpd
/etc/rc.d/rc5.d/S60lpd
/etc/rc.d/rc6.d/K60lpd
"""
```