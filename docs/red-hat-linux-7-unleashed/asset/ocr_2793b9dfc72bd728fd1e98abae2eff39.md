# # Shutting Down the Linux System

By now you've learned not only how Linux starts, but also a little bit about how it shuts down. If you look at the scripts in runlevel 0, you'll find a number of services being shut down, followed by the killing of all active processes, and finally, the halt script in `/etc/rc.d/init.d` directory executing the shutdown.

The halt script is used to either halt or reboot your system, depending on how it is called. What happens during a shutdown? If you're familiar with other operating systems (such as DOS), you remember that all you had to do was close any active application and then turn off the computer. Although Linux is easy to use, shutting down your computer is not as simple as turning it off. (You can try this, but you do so at your own risk.) A number of processes must take place before you or Linux turns off your computer. The following sections take a look at some of the commands involved.

# ## shutdown

Although many people use Linux as single users on a single computer, many of us use computers on either a distributed or shared network. If you've ever been working under a tight deadline in a networked environment, you know the dreadful experience of seeing a system is going down in 5 minutes! message from the system administrator. You might also know the frustration of working on a system on which the system administrator is trying to perform maintenance, suffering seemingly random downtimes or frozen tasks.

Luckily for most users, maintenance jobs are performed during off hours, when most people are home with their loved ones or fast asleep in bed. Luckily for sysadmins, this is the perfect time for system administration or backups, and one of the top reasons for the alt.sysadmin.recovery newsgroup.

The primary command to stop Linux is the **shutdown** command. Like most UNIX commands, shutdown has a number of options. A man page for the shutdown command is included with Red Hat Linux, but you can quickly read its command-line syntax if you use an illegal option, such as **-z**. Thanks to the programmer, here it is:

```
Usage:	shutdown [-kAhfncr] [-t secs] time [warning message]
	-a:	use /etc/shutdown.allow
	-k:	don't really shutdown, only warn.
	-r:	reboot after shutdown.
	-h:	halt after shutdown.
	-f:	 do a 'fast' reboot (skip fsck).
	-F:	Force fsck on reboot.
	-n:	 don't go through "init" but go down real fast.
	-C:	cancel a running shutdown.
	-t secs: delay between warning and kill signal.
	** the 'time' argument is mandatory! (try `now`) **
```