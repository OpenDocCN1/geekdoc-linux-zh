
![](img/43f64015de86d989e30eff5bb284fb96_621_0.png)

## Figure 13-10 The structure of the Logical Volume Manager

The boot loader (LILO or GRUB) is not able to work directly with LVM or a logical volume group, so if you want to have your root file system be part of a LVM (which is not uncommon), you need to create a separate /boot partition containing the Linux kernel. This partition would not be part of the logical volume group managed by the LVM utilities.

Suppose you have three hard disks that you want to use for a Linux system that is acting as a Web server. You create /boot and swap partitions, but use the majority of space on all three disks for two partitions: / and /www. The operating system will be stored on /, and all the Web server data will be stored on /www.

After using the system for several months, you realize that you need to add much more storage space to your Web server. First, you must shut down your server and install a fourth hard disk. After you restart, you can use the LVM utilities that are included with Linux to add the fourth hard disk to the logical volume group. Then you can increase the size of the /www partition without reformatting it or losing any data. This is something that was not possible with older hard disk management utilities.

If you create a logical volume group in Disk Druid as you install Linux, you can use the collection of LVM utilities to manage logical volume groups and make changes such as those described in the previous example. The lvm program is the principal utility; enter the command apropos lvm to see a list of related utilities.

## SYSTEM LOGS

On any ship, the captain keeps a log of information about each day, including where the ship has traveled, its cargo, and any noteworthy events. The log serves as a record not only for the captain and crew, but also for others who may need detailed information about the ship.

In much the same way, Linux keeps detailed records of events within the system. These records, known as log files, are created by many programs. As the system administrator, you can refer to the log files to determine the status of your system, watch for intruders, or look for data about a particular program or event. Table 13-2 lists some commonly logged events and the location of the corresponding log files. This section focuses on the main system log, which is typically located at /var/log/messages.

## Table 13-2 Commonly Logged Events and Their Log Files

| Event | Path and file name of the log |
|---|---|
| Main system messages | /var/log/messages |
| Web server transfers | /var/log/httpd/access_log |
| FTP server transfers | /var/log/xferlog |
| E-mail server information | /var/log/maillog |
| Automatic script executions | /var/log/cron |

Many different programs write messages to /var/log/messages. A message is a description of what is happening within a program. The message may report information (someone has logged in), a warning (someone tried to log in unsuccessfully), or a serious error indicating that a program is about to crash. Several sample messages are shown later in this section. A number of daemons—such as the Web server, e-mail server, and login security programs—write to the file, as does the Linux kernel itself. The messages from the kernel tell you about low-level system activities such as when devices are first initialized and when daemons are started by the kernel.

The messages file uses a standard format. Each line of the file makes up an individual log message. Each message, in turn, contains the following information:

- The date and time when the event being logged occurred (often called the timestamp)
- The host name (or computer name) of the system on which the event occurred
- The name of the program generating the log message
- The message text itself, which may be more than one line long

A few sample lines from a messages log file are shown here. Notice that the host name for all these messages is brighton, the name of someone's computer. Also notice that several different programs have generated the log messages shown here, including the Linux kernel, the httpd daemon (the Web server), the sound system, and other programs.

```
Oct 26 06:42:29 brighton kernel:
Installing knfsd (copyright (C) 1996 ok
Oct 26 06:42:29 brighton nfs: rpc.nfsd startup succeeded
Oct 26 06:42:29 brighton keytable: Loading keymap:
Oct 26 06:42:30 brighton keytable: Loading /usr/lib/kbd/keymaps/1386/qwe
Oct 26 06:42:30 brighton keytable: Loading systemfont:
Oct 26 06:42:30 brighton rc: Starting keytable succeeded
Oct 26 06:42:30 brighton gpm: gpm startup succeeded
Oct 26 06:44:57 brighton rpc.statd[451]:
gethostname error for brighto
Oct 26 06:45:01 brighton httpd: Cannot determine local host name.
Oct 26 06:45:01 brighton httpd:
Use the ServerName directive to set it
Oct 26 06:45:01 brighton httpd: httpd startup failed
Oct 26 06:45:01 brighton sound: Starting sound configuration:
Oct 26 06:45:01 brighton sound: sound
Oct 26 06:45:01 brighton rc: Starting sound succeeded
Oct 26 06:45:02 brighton PAM_pwdb[582]:
(su) session opened for user xfs
Oct 26 06:45:03 brighton PAM_pwdb[582]:
(su) session closed for user xfs
Oct 26 06:45:03 brighton xfs: xfs startup succeeded
Oct 26 06:45:05 brighton rc: Starting local succeeded
Oct 26 06:45:08 brighton PAM_pwdb[629]: check pass; user unknown
Oct 26 06:45:09 brighton login[629]:
FAILED LOGIN 1 FROM (null) FOR root, User not known to the
underlying authentication module
```

Right now you don't have to understand everything in the preceding log file lines. But you should become familiar with the format of a log line.

If you see a program in a log line that you don't recognize, you can use the whatis command to learn about it. This command looks at a database of program descriptions and prints a one-line description of the program you ask about. Sometimes the result is not too helpful, but it can give you a starting place and also refer you to a man page that may provide more information.

![](img/43f64015de86d989e30eff5bb284fb96_623_0.png)

The whatis command uses an internal database to find an answer to your query. That database should be prepared automatically, but if it is not available, you can create it by running the command makewhatis.

## The syslogd and klogd Daemons

A programmer writing software for Linux can rely on the programming function named syslog to write a message to the /var/log/messages file or another configured location, as described shortly. All of the calls to the syslog function are managed by syslogd, the system logging daemon.

The syslogd daemon watches for messages submitted by programs; another daemon called klogd (kernel logging daemon) watches for messages submitted by the Linux kernel. The klogd daemon logs kernel messages to /var/log/messages (or another configured location). Both klogd and syslogd write messages to the same log file. Figure 13-11 shows how everything works together to record log messages.

![](img/43f64015de86d989e30eff5bb284fb96_624_0.png)

Figure 13-11 syslogd and klogd work together to process log messages

The syslogd and klogd daemons are started by the system initialization scripts in /etc/rc.d/init.d each time you start your Linux system. You should never need to start these programs manually.

## Configuring the System Log

You can configure what information you want syslogd and klogd to store in the main system log (/var/log/messages by default) and what information you want stored in other files. Both syslogd and klogd rely on a single configuration file: /etc/syslog.conf. Figure 13-12 shows the format of each line in the syslog.conf file. The parts of the figure are described below it.

## Figure 13-12 The format of each line in /etc/syslog.conf

facility.priority ;facility.priority Action
Selector Optional additional selectors

As with most configuration files, lines that begin with a hash mark (#) in /etc/syslog.conf are comments and are ignored by the logging daemons.

Each line in the syslog.conf file contains two parts:

- A selector, a set of code words that selects what events are being logged
- An action, a file name or user name that determines either the file in which the message describing an event is written or the users on whose screen the message appears (the action can also refer to a remote computer for networked logging, as described later in this section)

Each selector describing an event to be logged is composed of two parts:

- The facility, a code word that specifies which type of program is being selected (the category of program providing the log entry)
- The priority, a code word that specifies the type of messages being selected for logging

Consider this example log configuration line:

```
daemon.info    /var/log/messages
```

The left part of the line contains a selector: daemon.info. The facility of this selector is daemon. The priority is info. So, messages from any daemon program with a priority of info or higher are selected by these code words. On the right, the line contains an action: /var/log/messages. This action is a file name, which specifies that messages selected by the daemon.info selector are written to the file /var/log/messages.

## The Facilities

When a Linux program wants to log a message, it issues a programming call to the syslog function. As part of that call, the program indicates its type, or category. For example, when the login program records a message about a user logging into the system, the login program specifies that the message is coming from an authentication (security-related) program. The syslogd daemon uses this category information to determine where to write the message, based on the syslog.conf configuration. The actual name of the program (login, in this example), rather than the category (authentication in this example), is written to the log file. Table 13-3 lists the different facilities, or types of programs, for which you can separately configure logging.
