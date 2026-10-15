
## Checking Your Log Files

Linux, like most UNIX systems, keeps a set of log files describing important system activity. One of the important tasks you face as a system administrator is to monitor these log files. In truth, this can be an extremely dull task because most of the log file entries are routine and uninformative. You normally don't really care that ferd logged onto the system at 9:38 AM on Monday, for instance. If, however, you know that ferd is on vacation in Nepal without Internet access, that login should raise a red flag as a potential security violation. Log files can also provide useful diagnostic information when you're installing new programs—and particularly new daemons, which typically log information rather than interact directly with you. You should therefore know something about log files and the tools you can use to help you keep abreast of them without boring you to tears.

## The syslogd Facility

Red Hat Linux uses a daemon called syslogd to handle system logging. In principle, it works like this: When a program wants to log a message, it sends that message to the system log daemon, which then writes the message to a file or passes it on to another system. This design allows even user programs to log messages in system files to which the calling user can't normally write because syslogd normally runs with root privileges.

You configure syslog by editing the /etc/syslog.conf file. The default configuration places most messages in /var/log/messages, but you can change this location. The system logger also handles a number of message types that don't go in /var/log/messages, but in other files. You should read the syslog.conf manpage for more information about the format of this file.

### NOTE

> Many commercial UNIXes place messages in /var/log/syslog rather than /var/log/messages, but the files serve much the same function.

Many programs (particularly daemons) have options to turn on or off system logging, or to log more or fewer messages. This characteristic can be quite handy if you're having problems because you can run the daemon with whatever options it requires to log debugging information. You can then examine the last few lines in /var/log/messages to discover what went wrong when a problem occurs. You might find that the daemon choked on a particular option in a configuration file, for instance, or that it received some input that didn't match its expectations.

In addition to or instead of using syslogd, some daemons create their own log files. Samba does this, for instance. Such log files often include information that’s not found in the /var/log/messages file, so you may want to check for log files specific to the service you’re investigating when you look for information.

## The /var/log Directory

Most Linux distributions store their most important log files in the /var/log directory by default. In order to prevent the log files from growing to a size that threatens to overrun your hard disk, distributions include cron jobs that run once a week, early on Sunday mornings, that rotate the log files. In Red Hat Linux, five log files are kept for each original: Four previous weeks’ files and one current file. (Other distributions may keep the same or different numbers of log files.) For instance, you’ll find in /var/log the current file messages along with the preceding weeks’ files messages.1, messages.2, messages.3, and messages.4. Each week, the cron job erases messages.4 and promotes each preceding week’s log up one number. A new messages file starts empty, but quickly begins to accumulate new messages.

### NOTE

Although the log files are rotated once a week, the cron job that accomplishes this task actually runs daily. It simply specifies a weekly rotation, and so does nothing six days out of seven. You can alter this behavior by editing the file /etc/logrotate.conf and changing weekly (near the top of the file) to daily, monthly, or size bytes to set daily, monthly, or size-based rotation schedules, respectively. See the logrotate manpage for more details.

### TIP

Most servers run 24 hours a day, 7 days a week, so this weekly cron job does its thing reliably. If for some reason you normally shut down your server on the weekend, though, you may want to either reconsider that policy or reschedule the cron job. Altering the log rotation to occur daily rather than weekly may be a good option if you leave the computer powered on overnight at least occasionally. Otherwise, you can create a cron job to run logrotate occasionally when the system is running, or you can run logrotate manually whenever it’s convenient.
