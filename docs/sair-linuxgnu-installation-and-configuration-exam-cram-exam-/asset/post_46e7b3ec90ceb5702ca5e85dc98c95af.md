
## Troubleshooting

Terms you'll need to understand:
- ✓ System message logging
- ✓ /etc/syslog.conf
- ✓ Read error
- ✓ Archive error
- ✓ Device full error
- ✓ badblocks
- ✓ Rescue disk
- ✓ Login and boot errors
- ✓ Keyboard repeat rate
- ✓ setleds
- ✓ Network Time Protocol (NTP)

Techniques you'll need to master:
- ✓ Finding shortcuts
- ✓ Mastering systematic analysis
- ✓ Understanding system log files
- ✓ Addressing installation errors
- ✓ Using rescue disks
- ✓ Solving boot errors
- ✓ Troubleshooting printer problems
- ✓ Updating system clocks
- ✓ Addressing memory issues
- ✓ Modifying keyboard parameters

When you want to solve a problem, you troubleshoot it. Sometimes you can use shortcuts that are at your fingertips; other times you need to diagnose problems systematically. Linux has extensive log files that can help you in the troubleshooting process. Log files, however, do no good if you encounter errors when you try to install, start, or log in to Linux. There are a number of techniques available to address installation and startup problems, including the use of the Linux boot floppy disk.

Troubleshooting is a topic almost as extensive as Linux itself. The topics covered in this chapter are limited to the topics that are addressed on the Sair Linux/GNU Installation and Configuration exam.

### Problem-Solving Philosophy

Almost every problem in Linux has a “simple” solution. But only the most experienced administrators know all of the simple solutions. If you can’t find an easy way to diagnose and address your problem, you need to think about your problem systematically, using the basic scientific method.

### Quick Tools

There is no substitute for experience when you need a quick solution. If you don’t have the experience, you can lean on others with experience. If you don’t have direct access to Linux experts, you do have access to documentation from a number of Linux experts. As you have seen in previous chapters, the documentation supporting Linux is extensive. If all else fails, you can usually contact those Linux experts who virtually prowl the newsgroups looking for problems to solve. Generally, if you have a problem, use the following steps to look for a quick solution:

1. Check applicable help switches. Almost every command includes extensive help switch output, which is available by typing `--help` after a command.
2. Study man pages. Every command, and a large number of configuration files, include manuals that help you understand the objectives of each command and switch.
3. Look through the HOWTOs and FAQs of the Linux Documentation Project at www.linuxdoc.org.
4. Examine knowledge or troubleshooting databases for your Linux distribution. Several distribution Web sites include a database of problems and solutions.
5. Search through newsgroup archives. Linux users share their experience through newsgroups. As discussed in Chapter 2, the easiest way to search through newsgroup archives is through the www.deja.com site.
6. If all else fails, ask for help on the appropriate Linux newsgroup. Be sure to document the work that you've done so far on the problem. If you don't get an answer to your question, you may need to clarify your situation further or try a different newsgroup.

Depending on your level of experience with Linux and knowledge of your particular problem, you may want to follow these steps in a different order.

> TIP
> if you need to ask a question on a newsgroup, be prepared. Experienced Linux users want to know that you've checked all available documentation. They'll want to know what else you've done to try to address your problem as well as the relevant portions of your configuration and log files. Providing this information is no different than what you would do when presenting your problem to an experienced Linux consultant.

### Scientific Method

You can ask for help on newsgroups, but answers take time. And if you're a Linux administrator with a problem, your users want immediate solutions. If you don't have a quick solution, your other option is to examine your problem using the scientific method.

There are three basic steps in the scientific method: analyze, theorize, and test. In other words, analyze your problem with all available data, theorize about the cause, and test your theory with a solution.

When you analyze a problem, you need to think systematically. For example, if you're having trouble sharing information with a Microsoft Windows computer, you might have a problem with your Samba daemon. But in general, you're more likely to have a problem with your basic network configuration. Furthermore, the most probable cause is a problem with your physical connections.

Systematic solutions require "bottom-up" thinking. For most unknown problems, you might check your system in the following order:

1. Check physical connections. Are the cables properly plugged in? Is each component getting power?
2. Check Linux connections. Does Linux recognize your problem hardware? Did Linux load your driver when you booted your computer?
3. Review applicable system logs. Are there errors or other information relevant to your problem?
4. Check basic software. Can you connect to problem hardware? Did Linux start the applicable daemon?
5. Check higher-level software. Can you actually communicate with key hardware components with various commands? What kind of error messages do you see when you use your software?

These are general steps to problem analysis. You can theorize about a cause at any point in the process. Most of the time, when you identify a cause (e.g., the network card is not connected), you can easily determine a solution (e.g., connect the network card). The actual steps you take depend on your problem and experience.

### System Logs

You can set up system logs in a number of categories including kernel, printer, mail, other daemons, and security (also known as auth). Messages are available in the following eight categories, listed in descending order of importance:

- emerg (emergency)
- alert
- crit (critical)
- err (error)
- warning
- notice
- info
- debug

### Log Locations

Whenever something happens in Linux, information is sent to system logs as defined in your /etc/syslog.conf configuration file. Perhaps the best organized /etc/syslog.conf file is from the Corel distribution, shown in Figure 14.1.

As shown in Figure 14.1, messages are divided in categories and subdivided by order of importance. Messages in each area are sent to a specific log file.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_283_0.png)

Review the /etc/syslog.conf and the log files available for your distribution. The contents of these files should help you understand the function of each log file.

```
# /etc/syslog.conf Configuration file for syslog.
#
# For more information see syslog.conf(5)
# manpage.
# syslog.conf changed by Brian
#
# authpriv and authpriv are combined
 authpriv, auth.*debug          /var/log/auth/auth.debug
 authpriv, auth.=info           /var/log/auth/auth.info
 authpriv, auth.=notice         /var/log/auth/auth.notice
 authpriv, auth.=warning        /var/log/auth/auth.warning
 authpriv, auth.=err            /var/log/auth/auth.err
 authpriv, auth.=crit           /var/log/auth/auth.crit
 authpriv, auth.=alert          /var/log/auth/auth.alert
 authpriv, auth.=emerg          /var/log/auth/auth.emerg
 cron.*debug                    /var/log/cron/cron.debug
 cron.=info                     /var/log/cron/cron.info
 cron.=notice                   /var/log/cron/cron.notice
 cron.=warning                  /var/log/cron/cron.warning
 cron.=err                      /var/log/cron/cron.err
 cron.=crit                     /var/log/cron/cron.crit
 cron.=alert                    /var/log/cron/cron.alert
 cron.=emerg                    /var/log/cron/cron.emerg
```

Figure 14.1 Excerpt from the /etc/syslog.conf message log configuration file.

### System Log Messages

System log messages can help you solve problems. Understanding which log file to use or review in each situation comes with experience. Take a look at Figure 14.2, which shows information messages in the daemon category (daemon.info). The last two messages shown indicate that Linux had a problem installing sound drivers for this particular computer.

You can find another useful set of messages with the dmesg command, which shows the sequence of events when you booted Linux on your computer.

### Installation Issues

There are a number of errors that you may encounter when installing Linux. In several cases, you may also have these problems when running Linux. These issues are related to problems with files or storage media.

```
Oct 11 08:46:27 Laptop cardmgr[222]: starting, version is 3.1.2
Oct 11 08:46:37 Laptop cardmgr[222]: watching 2 sockets
Oct 11 08:46:37 Laptop cardmgr[222]: initialising...
Oct 11 08:46:07 Laptop cardmgr[222]: socket 5: Serial or Modem
Oct 11 08:46:07 Laptop cardmgr[222]:   card: /etc/pcmcia/modules/2.2.12/pcmcia/serial_cs.o
Oct 11 08:46:07 Laptop cardmgr[222]: executing: /sbin/modprobe -s -k -o serial_cs
Oct 11 08:46:07 Laptop cardmgr[222]: initialising pcmcia scheme: No such file or directory
Oct 11 08:46:08 Laptop cardmgr[222]: socket 1: 3Com 3c589 Ethernet
Oct 11 08:46:08 Laptop cardmgr[222]:   card: /etc/pcmcia/modules/2.2.12/pcmcia/3c589_cs.o
Oct 11 08:46:08 Laptop cardmgr[222]: executing: /sbin/modprobe -s -k -o 3c589_cs
Oct 11 08:46:08 Laptop cardmgr[222]: initialising pcmcia scheme: No such file or directory
Oct 11 08:46:08 Laptop cardmgr[222]: can't locate module sound-slot-0
Oct 11 08:46:51 Laptop sndprobe: can't locate module sound-service=0-0
```

Figure 14.2 Sample system log messages.
