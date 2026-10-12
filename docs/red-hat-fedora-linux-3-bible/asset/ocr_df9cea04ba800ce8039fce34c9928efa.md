# Part III: Administering Fedora



```
# Don't log private authetication messages!
*.info;mail.none;news.none;authpriv.none;cron.none /var/log/messages
# The authpriv file has restricted access.
authpriv.* /var/log/secure
# Log all the mail messages in one place.
mail.* /var/log/maillog
# Log cron stuff
cron.* /var/log/cron
# Everybody gets emergency messages
*.emerg *
# Save news errors of level crit and higher in a special file.
ucp,news.crit /var/log/spooler
# Save boot messages also to boot.log
local7.* /var/log/boot.log
#
# INN
#
news.=crit /var/log/news/news.crit
news.=err /var/log/news/news.err
news.notice /var/log/news/news.notice
```

The lines beginning with a # character are comments. Other lines contain two columns of information, separated by spaces or tabs. The left field is a semicolon-separated list of message types and message priorities. The right field is the log file to which those messages should be written. To send the messages to another computer (loghost) instead of a file, simply replace the log file name with the @ character followed by the name of the loghost. For example, to redirect the output normally sent to the messages, secure, and maillog log files, make these changes to the previous file:

```
# Log anything (except mail) of level info or higher.
# Don't log private authetication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost
# The authpriv file has restricted access.
authpriv.* @loghost
# Log all the mail messages in one place.
mail.* @loghost
```

The messages will now be sent to the syslogd running on the computer named loghost. The name loghost was not an arbitrary choice. It is customary to create such a host name and make