ties and the kernel. There are many log files on a typical UNIX system, but we'll take a look at the most commonly used log file in this section called syslog.

Most log files appear in /var/log, one of its subdirectories, /var/adm, or one of its subdirectories. Unfortunately there is usually a little hunting around required to find log files. Almost all UNIX variants put log files somewhere under /var, so at least you have a place to start your search. Some log files require superuser rights to access, so you cannot read all log files on your system.

The most often used log file is syslog. It is called the system event logger because it is a comprehensive logging utility. It includes many facilities, so the kernel, mail system, printer spooler, cron, and many other programs can use it.

![](bbox=[0.03, 0.38, 0.12, 0.48])

syslog consists of several parts, including a daemon, library routines, and a logger. In all likelihood, your system is running the daemon called syslogd. You can check this with ps.

The result of using syslog is a log file that you can view should you encounter a problem with your system. You'll get messages of varying degrees of importance in syslog ranging from nothing more than informational messages to panic situations.

# dmesg

Another tool used to report system information is dmesg. It looks in the system buffer for recently printed diagnostic messages. It is most often used to print messages produced at the time of system boot. This capability is very helpful in determining what hardware exists on your system. You don't normally have to be superuser to run this command.

# The Kernel

The kernel is the heart of the UNIX system. Its configuration and maintenance are the domain of the system administrator. In this sec-