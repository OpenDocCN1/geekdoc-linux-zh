
+ lpr.info /var/log/lpd-errs
+ cron.* /var/log/cron
+ *.err root
+ *.notice;news.err root
+ *.alert root
+ *.emerg *

You can interpret this to mean that all **err** messages from any service, **debug** messages from the kernel, authorization **notice** messages, and **crit** messages from mail programs will be printed out to the system console, and you will see them if you have a monitor hooked up to your FreeBSD machine. Similarly, all security-related messages go into the `/var/log/security` file, and all messages from mail programs at the **info** level go into `/var/log/maillog`. Almost everything else goes into `/var/log/messages`, the general system log file. (If you’re used to Linux, this file is equivalent to what is usually called `syslog`.)

Certain types of messages are not merely written to log files but are sent to a variety of other types of handling mechanisms. In the default `syslog.conf`, messages from any service at the **err**, **notice**, or **alert** level are printed to any terminal where root is logged in, and **emerg** messages are printed to all users at all terminals. Table 10.4 shows the possible actions for `syslogd` messages and the syntax for each.

### TABLE 10.4 Syntaxes for syslogd Actions

| Syntax | Action Taken |
| :--- | :--- |
| `/path/to/file` | Messages are written to the specified file. |
| `@some.hostname.com` | Messages are forwarded to `syslogd` at `some.hostname.com` using the `syslog` network service. |
| `user1` | Messages are printed to any terminal where `user1` is logged in. |
| `root,user1,user2` | All specified users receive messages on all their terminals. |
| `*` | Messages are written to all logged-in users. |
| `\| "mail root"` | Messages are mailed to root. |

Further details on how to configure `syslogd` can be found in the man `syslogd` and man `syslog.conf` pages.

> **NOTE**
> Each log file in `/var/log` is rolled over according to a different set of rules. For instance, the `/var/log/maillog` file is archived and restarted every day by the `periodic` program. Other log files, such as `/var/log/cron` and `/var/log/messages`, are refreshed through other means (often internally by the programs that write to them). Archived log files are generally compressed with `gzip`. To search through old log files, use `gzcat` in conjunction with the conventional `grep`: `# gzcat /var/log/messages.2.gz | grep "rejected"`

## Notes on the /etc/rc.local File

The resource configuration script /etc/rc.local was described earlier in this chapter simply as being obsolete. Administrators who used earlier versions of FreeBSD or certain Linux distributions will recognize this file. Its purpose is much the same as the /usr/local/etc/rc.d directories—to provide you with a mechanism to extend the system’s startup behavior.

The rc.d method described earlier is the preferred method of accomplishing the extending of system startup behavior because it’s a more structured method. It keeps each startup task in its own script with a common interface—corralled into /usr/local and out of /etc. If you must use it, however, /etc/rc.local still works, although it doesn’t exist in the default installation. You can create the file (with the proper interpreter line modeled after the other rc.* files) and put any set of shell commands into it, and it will be executed just before the rc.d scripts.

Support for rc.local is for backward compatibility only, and it may eventually be removed from FreeBSD. To make sure your system supports it, check /etc/rc for mention of the rc.local file, as shown in Listing 10.3.

**LISTING 10.3 Excerpt from /etc/rc Showing Support for /etc/rc.local**

```bash
# grep -A 5 rc.local /etc/rc
# Do traditional (but rather obsolete) rc.local file if it exists. If you
# use this file and want to make it programmatic, source /etc/defaults/rc.conf
# in /etc/rc.local and add your custom variables to /etc/rc.conf, as
# shown below. Please do not put local extensions into /etc/rc itself.
# Use /etc/rc.local
#
# --- rc.local ---
#	if [ -r /etc/defaults/rc.conf ]; then
#		./.etc/defaults/rc.conf
#	source_rc_confs
#	elif [ -r /etc/rc.conf ]; then
#		./.etc/rc.conf
--
# --- rc.local ---
#
if [ -r /etc/rc.local ]; then
	echo -n 'starting local daemons:'
	sh /etc/rc.local
	echo '.'
fi

# For each valid dir in $local_startup, search for init scripts matching *.sh
#
```

The loop that runs `sh /etc/rc.local` is what you're looking for. If it's there and not commented out, you can use `rc.local`. It is still a much better idea, however, to use the `rc.d` script method.

# CHAPTER 11
## Customizing the Shell

Regardless of whether you choose to operate your FreeBSD system through the X-Window GUI—particularly as an administrator—you’re going to have to deal with a shell. A shell gives you all the flexibility you need to accomplish even the most complex tasks but also dictates a user experience that’s arcane at best. In this chapter, we’ll make ourselves at home in the shell—comfortable enough to use it as a programming environment and as a user interface.

### What Is a Shell?

We’ve already talked about the basics of the shell and what you can do with it back in Chapter 7, “Working with the Shell.” That chapter introduced the shell as a command-line interface and discussed the various shells you can use in FreeBSD and what kinds of commands are available in the shell for controlling the system. Now, we’ll be looking at the shell itself in more detail and examining how it applies to the multitudes of users you might be supporting on your system and how to customize it to your taste.

You already know that a shell (in brief) is a command-line interface in which you can enter the typed commands that make the Unix computing experience so markedly different from a fully GUI-based one such as Windows or Mac OS. The shell is similar in function to the COMMAND.COM command interpreter in MS-DOS and its descendants in Windows, but it’s vastly more complex and useful because it plays a much more important role than in a GUI-based operating system.

But why is it called a shell? The answer has to do with the terminology used in Unix architecture to describe the various levels of system operation in terms of a multilayered ball, with the most automated functions at the core and the user-triggered functions on the outer layer. On the inside is the kernel, which has been mentioned in earlier chapters and will be covered thoroughly in Chapter 17, “Kernel Configuration.” On the outside of the system is the user. How does the user interact with the kernel and its surrounding support programs? Through the shell, naturally. This relationship is illustrated in Figure 11.1.

![](img/48eec858cce7dfb89da36a4d40b7daf3_265_0.png)

**FIGURE 11.1** The kernel surrounded by the shell.

The job of the shell is to give you—the user—a safe, structured way to access the kernel. As a command interpreter, the shell takes your commands and translates them into processes that access files and devices through the kernel. It prevents you from executing unsafe code that could crash the kernel, and it helps you find and execute the programs that run the system.

In a more practical sense, the shell is simply a forking-capable utility that is executed by the system whenever you log in. The shell presents you with a command prompt, interprets your commands, and terminates when you log out. In fact, these are the only things a shell really needs to do; any program can act as a shell, which is a fact that can be used with great creativity, as you will see.

You probably will encounter the term shell used in a number of slightly different contexts. For instance, any program running on top of another and providing an interface to it is a type of shell; Windows 95 is technically a shell, albeit a better-disguised one than its

### IN THIS CHAPTER

- What Is a Shell?
- Adding Shells to the System and Making Them Available
- Using Alternate Shells
- Shell Initialization Files
- Customizing Your Shell Environment
- Shell and Environment Variables
