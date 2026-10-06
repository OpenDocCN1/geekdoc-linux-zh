# Dealing with Runlevels and the Initialization Process

| TABLE 5.1 Runlevels and their purposes |
| Runlevel | Purpose |
| --- | --- |
| 0 | A transitional runlevel, meaning that it is used to shift the computer from one state to another. Specifically, it shuts down the system. On modern hardware, the computer should completely power down. If not, you're expected to reboot the computer manually or power it off. |
| 1, s, or S | Single-user mode. What services, if any, are started at this runlevel varies by distribution. It's typically used for low-level system maintenance that may be impaired by normal system operation, such as resizing partitions. |
| 2 | On Debian and its derivatives, a full multi-user mode with X running and graphical login. Most other distributions leave this runlevel undefined. |
| 3 | On Fedora, Mandriva, Red Hat, and most other distributions, a full multi-user mode with a console (non-graphical) login screen. |
| 4 | Usually undefined by default and therefore available for customization. |
| 5 | On Fedora, Mandriva, Red Hat, and most other distributions, the same behavior as runlevel 3 with the addition of having X with an XDM (graphical) login. |
| 6 | Used to reboot the system. This runlevel is also a transitional runlevel. Your system is completely shut down, and then the computer reboots automatically. |

> > Dont configure your default runlevel to 0 or 6. If you do, your system will immediately shut down or reboot once it finishes powering up. Runlevel 1 could conceivably be used as a default, but chances you'll want to use 2, 3, or 5 as your default runlevel, depending on your distribution and use for the system.

As a general rule, distributions have been drifting toward Red Hat's runlevel set; however, there are exceptions and holdouts, such as Debian. Distributions that use startup systems generally don't use runlevels natively, but they provide compatibility tools that make the computer appear to use runlevels for the benefit of scripts and programs that assume the use of runlevels.

# Identifying the Services in a Runlevel

There are two ways to affect what programs run when you enter a new SysV runlevel. The first is to add or delete entries in your /etc/initabb file. A typical /etc/initabb file contains many entries, and for a couple of special cases, inspecting or changing the contents of this file is best left to experts. Once all the entries in /etc/initabb for your runlevel are executed, your boot process is complete, and you can log in.