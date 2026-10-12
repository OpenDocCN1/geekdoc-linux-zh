```
# Save news errors of level crit and higher in a special file.
uucp,news.crit /var/log/spooler
# Save boot messages also to boot.log
local7.* /var/log/boot.log
#
# INN
#
news.=crit /var/log/news/news.crit
news.=err /var/log/news/news.err
news.notice /var/log/news/news.notice
```

The lines beginning with a # character are comments. Other lines contain two columns of information, separated by colons (spaces won't work). The left field is a semicolon-separated list of message types and message priorities. The right field is the log file to which those messages should be written. To send the messages to another computer (the loghost) instead of a file, simply replace the log file name with the @ character followed by the name of the loghost. For example, to redirect the output normally sent to the messages, secure, and maillog log files, make these changes to the above file:

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost
# The authpriv file has restricted access.
authpriv.* @loghost
# Log all the mail messages in one place.
mail.* @loghost
```

The messages will now be sent to the syslogd running on the computer named loghost. The name loghost was not an arbitrary choice. It is customary to create such a host name and make it an alias to the actual system acting as the loghost. That way, if you ever need to switch the loghost duties to a different machine, you only need to change the loghost alias; you do not need to recdlt the syslog. conf file on every computer.

# Understanding the messages logfile

Because of the many programs and services that record information to the messages logfile, it is important that you understand the format of this file. Examining this file will often give you a good early warning of problems developing on your system. Each line in the file is a single message recorded by some program or service. Here is a snippet of an actual messages log file:

```
Feb 25 11:04:32 toys network: Brining up loopback interface: succeeded
Feb 25 11:04:35 toys network: Brining up interface etho: succeeded
Feb 25 13:01:14 toys vsftpd(pam_unix)[10565]: authentication failure;
loginme= uid=0 euid=0 tty= ruser= rhost=10.0.0.5 user=chris
```