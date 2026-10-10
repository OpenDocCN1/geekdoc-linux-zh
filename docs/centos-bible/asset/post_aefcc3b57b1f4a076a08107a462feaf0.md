
service may be easier than typing in a long list of subnets or domains, but better a few minutes spent on proper security measures than many hours recovering from a break-in.

> You can further restrict access to services using various options within the `/etc/xinetd.conf` file, even to the point of limiting access to certain services to specific times of the day. Read the manual page for xinetd by typing `man xinetd` at a command prompt to learn more about these options.

## Checking Log Files

Preparing your system for a cracker attack is only part of the battle. You must also recognize a cracker attack when it is occurring. Understanding the various log files in which CentOS records important events is critical to this goal. The log files for your CentOS system can be found in the `/var/log` directory.

Because the system logs are plaintext files, you can view the contents of logs directly using any text editor or paging command (such as `less` or `more`). The `logwatch` facility that comes with CentOS sends daily highlights from your log files in an e-mail message to the `root` user. You can also add packages, such as `logsentry`, to monitor your log files.

## Replacing the `syslogd` Package

The default logging service in CentOS is `syslogd`. However, the newer `rsyslogd` is more flexible and powerful than its predecessor. I suggest that you install and use `rsyslogd`, and uninstall `syslogd`. You can do this at a Terminal window as `root` user.

```bash
# yum install rsyslog && yum remove syslogd
```

The `&&` is very important because removing the `syslogd` package without having a `syslog` replacement will remove most of your system!

After the `rsyslog` package has been installed with `yum`, you need to enable it with `chkconfig` and start the service.

```bash
# service rsyslog start
# chkconfig rsyslog on
```

## Understanding the `rsyslogd` Service

Most of the files in the `/var/log` directory are maintained by the `rsyslogd` service. The `rsyslogd` daemon is the System Logging Daemon and acts as an extension of a previous logging system called `syslogd`. It accepts log messages from a variety of other programs and writes them to the appropriate log files. This is better than having every program write directly to its own log file because it allows you to centrally manage how log files are handled. It is possible to configure rsyslogd to record varying levels of detail in the log files. It can be told to ignore all but the most critical message, or it can record every detail.

The rsyslogd daemon can even accept messages from other computers on your network. This is particularly handy because it enables you to centralize the management and reviewing of the log files from many systems on your network. There is also a major security benefit to this practice. If a system on your network is broken into, the cracker cannot delete or modify the log files because those files are stored on a separate computer.

It is important to remember, however, that those log messages are not, by default, encrypted. Anyone tapping into your local network will be able to eavesdrop on those messages as they pass from one machine to another. Also, although the cracker may not be able to change old log messages, she will be able to affect the system such that any new log messages should not be trusted.

It is not uncommon to run a dedicated loghost, a computer that serves no other purpose than to record log messages from other computers on the network. Because this system runs no other services, it is less likely that it will be broken into. This makes it nearly impossible for the cracker to erase her tracks. It does not, however, mean that all of the log messages are accurate after a cracker has broken into a machine on your network.

## Re-Directing Logs to a loghost with rsyslogd

To re-direct your computer's log files to another computer's rsyslogd, you must make some changes to your local rsyslogd's configuration file. The file that you need to work with is `/etc/rsyslog.conf`. If you are not already root, become root and then open the `/etc/rsyslog.conf` file in a text editor (such as `vi`). You should see something similar to this:

```text
# Log all kernel messages to the console. # Logging much else clutters up the screen. #kern.* /dev/console
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none /var/log/messages
# The authpriv file has restricted access.
authpriv.* /var/log/secure
# Log all the mail messages in one place.
mail.* -/var/log/maillog
# Log cron stuff
cron.* /var/log/cron
# Everybody gets emergency messages
*.emerg *
# Save news errors of level crit and higher in a special file.
uucp,news.crit		/var/log/spooler
# Save boot messages also to boot.log
local7.*			/var/log/boot.log
```

The lines beginning with a `#` character are comments. Other lines contain two columns of information, separated by spaces or tabs. The left field is a semicolon-separated list of message types and message priorities. The right field is the log file to which those messages should be written.

> **NOTE**
>
> Notice the dash (`-`) before the `/var/log/maillog` file. Normally, each log file is synced after every logging. A dash preceding the full path to the log file indicates that the file is not synced after each logging. While this might result in lost information if your machine crashes before the log is written, it can result in better performance on your system if you run verbose logging.

To send the messages to another computer (the loghost) instead of a file, simply replace the log filename with the `@` character followed by the name of the loghost. For example, to re-direct the output normally sent to the messages, secure, and mailog log files, make these changes to the previous file:

```text
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none:cron.none		@loghost

# The authpriv file has restricted access.
authpriv.*			@loghost

# Log all the mail messages in one place.
mail.*			@loghost
```

The messages will now be sent to the rsyslogd running on the computer named loghost. The name loghost was not an arbitrary choice. It is customary to create such a hostname and make it an alias to the actual system acting as the loghost. That way, if you ever need to switch the loghost duties to a different machine, you need to change only the loghost alias; you do not need to re-edit the rsyslog.conf file on every computer.

## Understanding the Messages Log File

Because of the many programs and services that record information to the messages log file, it is important that you understand the format of this file. Examining this file often gives you a good early warning of problems developing on your system. Each line in the file is a single message recorded by some program or service. Here is a snippet of an actual messages log file:

```text
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vsftpd[pam_unix] [10565]: authentication failure;
logname= uid=0 euid=0 tty= user= root= 10.0.0.5 user=chris
Feb 25 14:44:24 toys su(pam_unix) [11439]: session opened for user root by chris (uid= 500)
```

This is really very simple when you know what to look for. Each message is divided into five main parts. From left to right they are:

- The date and time that the message was logged
- The name of the computer that the message came from
- The program or service name that the message pertains to
- The process number (enclosed in square brackets) of the program sending the message
- The actual text message itself

Let's examine the previous file snippet. In the first two lines, you can see that I restarted the network. The next line shows that I tried to log in as the user named chris to get to the FTP server on this system from a computer at address 10.0.0.5. (I typed the wrong password, and authentication failed.) The last line shows that I used the `su` command to become root user.

By occasionally reviewing the messages file and the secure file, it is possible to catch a cracking attempt before it is successful. If you see an excessive number of connection attempts for a particular service, especially if they are coming from systems on the Internet, you may be under attack.

## Tracking Log Messages with logwatch

Another way to keep up with the contents of your log files is with the logwatch facility. logwatch flags messages that might reflect a problem with your system and forwards them each day in an e-mail message to your system's root user. When you install CentOS, the logwatch package is installed and configured to watch your log files and report suspicious activities to your system administrator. Based on the logwatch cron file (`/etc/cron.daily/ilogwatch`), the logwatch facility will:

- Run each morning at 4:00 a.m.
- Choose which log files to scan and where to send the e-mail message, based on the configuration file `/etc/logwatch/conf/logwatch.conf`. (The defaults are listed in `/usr/share/logwatch/default.conf`)
- Send an e-mail message to the local computer's root user that reports potentially suspicious activity on your system, based on the contents of your log files.
- Report on administrative activities that could reflect a problem with the system.

The kind of information logwatch reports on includes users and groups that have been deleted, packages installed or uninstalled, and disk space consumed. The daily messages also show login activity through ssh over the network and file transfer activities. Failure messages are flagged and reported for each log file scanned.
