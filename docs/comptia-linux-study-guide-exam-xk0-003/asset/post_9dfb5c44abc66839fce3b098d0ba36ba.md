
signal, which is more likely to work but can be more disruptive because the program may leave temporary files lying about and be unable to save changes to open files. The `-t time` parameter tells `telinit` how long to wait between sending these two signals to a process. The default is 5 seconds, which is normally plenty of time.

One special case of runlevel change happens when you are shutting down the computer. Runlevel 0 shuts down the computer and halts it; depending on kernel options and hardware capabilities, this may shut off power to the computer, or it may simply place the computer in a state from which it’s safe to turn off system power. Runlevel 6 reboots the computer. You can enter these runlevels using `telinit`, but it’s better to use a separate command called `shutdown` to accomplish this task because it offers additional options. The syntax for this command is as follows:

```
shutdown [-t sec] [-arhckfF] time [warning-message]
```

Table 4.2 describes the meanings of the parameters.

### TABLE 4.2: shutdown Options and Their Meanings

| Option | Meaning |
| :--- | :--- |
| -c | If you initiate a shutdown sometime in the future but then change your mind, issuing shutdown again with this parameter cancels it. |
| -h | This parameter causes the system to halt or power off after a shutdown. Which one occurs is up to the system. (When the system halts, the power stays on, but the OS has terminated. You can typically then power down via a power switch or use the Reset button to reboot the computer.) |
| -H | This parameter causes the system to halt after a shutdown, but not power off. |
| -k | This parameter “fakes” a shutdown—it sends a shutdown warning message to users, but it doesn’t shut down the computer. |
| -P | This parameter causes the system to power off after a shutdown. |
| -r | This parameter causes a reboot after a shutdown. Essentially, it invokes a change to runlevel 6. |
| time | Shutdowns may be scheduled with this parameter, which can take many different formats. One common value is now, which causes an immediate shutdown. You can also specify a time in 24-hour hh:mm format, as in 13:15 for a shutdown at 1:15 p.m. A time in the format +m causes a shutdown in m minutes. |
| warning-message | When many people use a system for remote logins, it’s generally a good idea to give these users advance warning of a shutdown. You can include a message explaining why the system is going down or how long you expect it to be down. |

The parameters to shutdown have changed over the years. Thus, you may find that your version of shutdown has extra parameters or lacks some of those specified in Table 4.2.

On a single-user system, `shutdown -h now` and `shutdown -r now` are perfectly reasonable uses of shutdown. When the system has many users, you might be better off scheduling a shutdown for 5, 10, or more minutes in the future and giving information on the expected downtime, as in the following:

```
# shutdown -h +10 "adding new hard disk; up again in 30 minutes"
```

Most modern distributions include commands called `halt` and `reboot` that are equivalent to `shutdown -h now` and `shutdown -r now`, respectively.

## Permanently Changing the Runlevel

You can permanently change the computer’s runlevel by editing the /etc/inittab file. This file contains a line like the following:

```
id:3:initdefault:
```

This example shows a system configured for runlevel 3. To modify it, you’d change the 3 to whatever value is appropriate. After making this change, you can cause the system to switch immediately to the new runlevel by running `telinit`, as described in the previous section. Typing `telinit 0` will cause the system to read your changes directly, or you can use the runlevel in place of 0.

Do not set the default runlevel to 0 or 6 since this will cause the system to shut down or reboot as soon as it boots.

## Real World Scenario: Using Upstart

The Linux init program is the first process that’s launched by the kernel. The traditional version of this program is controlled by /etc/inittab and sets the runlevel, launches the login process on several virtual terminals, and starts a few other low-level services. Most Linux systems work fine with a default configuration, with the possible exception of needing to change the runlevel.

Recently, though, the traditional Linux init program has been replaced by a new version in some distributions, including Ubuntu and Fedora. This new version, although it still includes init and telinit commands, goes by a new package name: Upstart (http://upstart.ubuntu.com). The Upstart versions of init and inittab work much like the traditional versions of these tools for most purposes; however, for Upstart, the /etc/inittab file is optional. If this file is present, it sets the default runlevel but is otherwise unused. Thus, you can set the default runlevel using /etc/inittab on an Upstart-based system, but if you’re accustomed to using /etc/inittab for other purposes, you’ll find that your usual /etc/inittab tweaks no longer work.

Instead of using /etc/inittab to launch login consoles and other tools, Upstart uses the /etc/event.d directory. This directory holds files, each of which describes the conditions for starting and stopping particular init-managed services. Chances are you won’t need to change these files, but you can do so if you need to alter your virtual terminal configuration, change how the system responds to the Ctrl+Alt+D keystroke, or do other things that were handled by /etc/inittab in the past.

## Configuring Log Files

Linux maintains log files that record various key details about Linux operation. Using these log files is described later, in “Using Log Files.” You may be able to begin using log files immediately, but knowing how to change the log file configuration can also be important. You do this by configuring the syslog daemon, although some servers and other programs perform their own logging and so must be configured independently. You may even want to configure one computer to send its log files to another system as a security measure. You should also be aware of issues surrounding log file rotation; if your computer doesn’t properly manage existing log files, they can grow to consume all available disk space on the partition on which they’re stored.

### Understanding syslogd

Most Linux systems employ a special daemon to handle log maintenance in a unified way. The traditional Linux system logger is syslogd, which is often installed from a package called syslogd. The syslogd daemon handles messages from servers and other user-mode programs; it’s usually paired with a daemon called klogd, which handles kernel messages and is usually installed from the same syslogd package as syslogd.

> **NOTE** Other choices for system loggers exist. For instance, syslog-ng is a replacement that supports advanced filtering options, and metaLog is another option. This chapter describes the traditional syslogd logger. Others are similar in principle, and even in some specific features, but differ in many details.

The basic idea behind a system logger is to provide a unified means of handling log files. The daemon runs in the background and accepts data delivered from servers and other programs that are configured to use the log daemon. The daemon can then use information provided by the server to classify the message and direct it to an appropriate log file. This configuration enables you to consolidate messages from various servers in a handful of standard log files, which can be much easier to use and manage than potentially dozens of log files from the various services running on the system.

As described in the upcoming section “Using a Remote Server for Log Files,” another feature of log daemons is that they can pass the log information on to a log daemon running on another computer entirely. The advantage of this configuration is that it can help protect the logs from tampering—if a computer is compromised, the intruder can't eliminate evidence of the intrusion from the log file without first breaking into the computer that logs data for other systems. Administering a network on which all systems log to a single system can also be simpler in some ways, because you can monitor log files on one computer, rather than perform this task on many systems.

In order to work, of course, the log daemon must be configured. In the case of syslogd, this is done through the /etc/syslog.conf file. The next section describes this file's format in more detail.

### Setting Logging Options

The format of the /etc/syslog.conf file is conceptually simple but provides a great deal of power. Comment lines, as in many Linux configuration files, are denoted by a hash mark (#). Noncomment lines take the following form:

```
facility.priority  action
```

In this line, facility is a code word for the type of program or tool that has generated the message to be logged; priority is a code word for the importance of this message; and action is a file, remote computer, or other location that's to accept the message. The facility and priority are often referred to collectively as the selector.

Valid codes for facility are auth, authpriv, cron, daemon, kern, lpr, mail1, mark, news, security, syslog, user, uucp, and local0 through local7. Many of these names refer to specific servers or program classes. For instance, mail servers and other mail-processing tools typically log using the mail facility. Most servers that aren't covered by more specific codes use the daemon facility. The security facility is identical to auth, but auth is the preferred name. The mark facility is reserved for internal use. An asterisk (*) refers to all facilities. You can specify multiple facilities in one selector by separating the facilities with commas (,).

Valid codes for priority are debug, info, notice, warning, warn, error, err, crit, alert, emerg, and panic. The warning priority is identical to warn, error is identical to err, and emerg is identical to panic. The error, warn, and panic priority names are deprecated; you should use their equivalents instead. Other than these identical pairs, these priorities represent ascending levels of importance. The debug level logs the most information; it's intended, as the name implies, for debugging programs that are misbehaving. The emerg priority logs the most important messages, which indicate very serious problems. When a
