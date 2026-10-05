# Using Log Files

to such problems, and terminating the leaking program can restore system performance to normal.

The free command supports several options, most of which modify its display format. The most useful of these is -m, which causes the display to use units of mebibytes (MiB) rather than the default of kibibytes (KiB).

# Using Log Files

Many programs that run in the background (daemons) write information about their normal operations to log files, which record such notes. Consulting log files can be an important part of diagnosing problems with daemons. The first step in doing this is to locate your log files. In some cases, you may need to tell the program to produce more-verbose output to help track down the problem. In this section, you'll learn some pointers on how to do that. Finally, this section describes the kernel ring buffer, which isn't technically a log file but can fill a similar role for kernel information.

# Logging Log Files

Linux stores most log files in the /var/log directory tree. Table 9.2 summarizes some log files on many Linux systems. In addition, many server programs not described in this book add their own log files or subdirectories of /var/log. If you experience problems with such a server, checking its log files can be a good place to start troubleshooting.

TABLE 9.2 Important log files

| Log file | Contents |
| --- | --- |
| boot.log | This file summarizes the services that are started in the boot process via SysV startup scripts |
| cron | This file summarizes processes that are run at regular intervals via the cron daemon. Although this book doesn't cover cron, a problem with it can cause glitches that recur at regular intervals, so you should be aware of it. |
| cups/ | This directory holds log files related to the Linux printing system. |
gdm/ | This directory holds log files related to the GNOME Display Manager (GDM), which handles GUI logins on many systems. |

Certification Objective

Log file details vary between distributions, some of the files in Table 9.2 may not be present on your system, or the files that you may find different names.

(Continues)