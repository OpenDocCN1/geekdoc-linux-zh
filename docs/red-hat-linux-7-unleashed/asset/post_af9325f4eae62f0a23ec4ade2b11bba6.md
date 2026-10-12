
## Runlevel 6: /etc/rc.d/rc6.d

Runlevel 6 is the reboot runlevel. The contents of this directory contain links similar to those in runlevel 0, but logic in the halt script under init.d determines whether the system is being shut down or rebooted.

Keeping track of which process is started or stopped in which runlevel can be difficult. In the next section you'll see one more reason why using Red Hat Linux can make your system administration tasks easier.

### 1. **linuxconf and Managing Your Services**

One of the great things about Red Hat Linux is the number of tools included in the distribution to help you manage your system. One important tool is Jacque Gelinas's `linuxconf`, which can be called from a command line in a terminal window while you're running X, from the command line of your console screen, or through your favorite Web browser. You should use `linuxconf` for a number of reasons:

- `linuxconf` provides a comprehensive graphic interface for administering your Red Hat system.
- You can save different system configurations, allowing you, for example, to set up your computer as a desktop machine or Internet server at different times with a single command line.
- `linuxconf` replaces and maintains a number of user, file, and network utilities (such as the old usercfg, fstool, and cabalet); the program is used as a configuration tool and service activation tool.
- `linuxconf` has the capability to use modules to add new features or capabilities.
- The program features built-in help for many services or actions.
- `linuxconf` allows system maintenance over a network, enabling more efficient management of in-house or remote computers and networks.

`linuxconf` is found under the /bin directory and weighs in at nearly 950,000 bytes. The program, written with more than 80,000 lines of C++ code, also comes with a support directory, /usr/lib/linuxconf, containing nearly 32MB of data, help files in several languages, and code modules.

After you log in as the root operator, start the `linuxconf` program from the command line with the following and press the Enter key:

```
# linuxconf
```

When you first run `linuxconf` you'll see a dialog of help text. If you're running X, have installed the GNOME software libraries, and run `linuxconf` a second time, the program's main window will appear as shown in Figure 9.1. Note that you can also use `linuxconf` without running X.

When used without GNOME libraries or from the console, the program (which started life as a configuration tool for the XFree86 X11 distribution) responds to keyboard commands just like Red Hat's Linux installation tool. Navigate around the program's dialog box by pressing the Tab key and then use the Enter key when the cursor is on a desired button or item in a list.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_291_0.png)

`linuxconf` can be used not only interactively, but also from the command line. The following related commands (and perhaps others by the time you read this) will be found in your filesystem after you install `linuxconf` (part of Red Hat Linux since version 5.1):

- `dnsconf`—A utility that can be used to configure a domain name server
- `fixperm`—A utility that checks system file permissions
- `fsconf`—A utility that manipulates the filesystem table, /etc/fstab, as shown in Figure 9.2.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_292_0.png)

- `mailconf`—A utility that configures the sendmail daemon
- `netconf`—A TCP/IP services configuration utility, as shown in Figure 9.3

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_292_1.png)

- `userconf`—User and group configuration (to add or delete users and groups)

Each program is a symbolic link to `linuxconf`. For example, to delete the user `clobie` from the command line, use `linuxconf`’s symbolic link `userconf`:

```
# userconf --deluser clobie
```

You can get help for each utility by using the `-help` command-line option, or if using X11, by clicking the Help button in the utility’s main dialog box.

The `linuxconf` command will also help you properly start and stop services under Linux while the **system is running**. Although you can selectively “kill” processes with the following code, where *pid* is the number of the running process, this is a crude, ineffective, and potentially harmful way to stop processes and system services.

`# kill -9 pid`

However, based on the information you have learned so far about the *init* scripts, you can use the following approach to stop the *httpd* Web server (as an example):

`# /etc/rc.d/init.d/httpd init stop`

Both of these are manual approaches, but the Red Hat folks have taken great pains to make system administration easier, so why not take advantage of menu convenience? When you use `linuxconf`, you can see at one glance which processes are going to be enabled or disabled.

> **Note**
>
> Other tools included with Red Hat Linux include `ntsysv` and `tksysv`, which may be used to control what services are started automatically during *boot up*, or to reassign services to different *runlevels*.

If you manually configure your system’s services by hand editing configuration files, be careful—making changes to default *runlevels* in `/etc/inittab` or indiscriminately using administration tools to change services or *runlevels* can put your system into an unusable state. If you run into trouble, reset your computer and enter *runlevel* 1.

Booting into single-user mode might allow you to fix any problems (a similar approach to another operating system’s “safe mode”). When you boot into single-user mode, you go directly into a *root* operator command line, which is handy for enabling a quick fix or performing other system administration tasks.

You should also know that `linuxconf` is a work in progress; not every item in the program is documented or has an associated Help menu or complete help text. For some additional details about `linuxconf`, tips on using modules, or other errata, see `linuxconf`’s home page at [http://www.solucorp.qc.ca/linuxconf/](http://www.solucorp.qc.ca/linuxconf/).

You can also subscribe to the `linuxconf` mailing list, `linuxconf@hub.xc.org`, or read archives of discussions about `linuxconf` through this site.

## Shutting Down the Linux System

By now you've learned not only how Linux starts, but also a little bit about how it shuts down. If you look at the scripts in runlevel 0, you'll find a number of services being shut down, followed by the killing of all active processes, and finally, the halt script in `/etc/rc.d/init.d` directory executing the shutdown.

The halt script is used to either halt or reboot your system, depending on how it is called. What happens during a shutdown? If you're familiar with other operating systems (such as DOS), you remember that all you had to do was close any active application and then turn off the computer. Although Linux is easy to use, shutting down your computer is not as simple as turning it off. (You can try this, but you do so at your own risk.) A number of processes must take place before you or Linux turns off your computer. The following sections take a look at some of the commands involved.

### shutdown

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
