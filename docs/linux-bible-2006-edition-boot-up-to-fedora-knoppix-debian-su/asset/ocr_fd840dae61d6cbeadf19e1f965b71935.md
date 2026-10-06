although the cracker may not be able to change old log entries, he can affect thensystem such that any new log messages should not be trusted.

It is not uncommon to run a dedicated loghost, a computer that serves no other
purpose to record log messages from other computers on the network.
Because this system runs no other services, it is unlikely that it will be broken into.
This makes it nearly impossible for a cracker to erase his or her tracks, but it does
not mean that all of the log entries are accurate after a cracker has broken into a
machine on your network.

# Redirecting Logs to a Loghost with syslog

To redirect your log files to another computer's syslog, you may make
changes to your local syslog configuration file. /etc/syslog.conf.
Become root using the su - command and then the /etc/syslog.conf file in
a text editor (such as vi). You should see something similar to this:

```
@ Log all kernel messages to the console.
# Logging much else clutters up the screen.
/dev/console
#kern.*
n# Log anything (except mail) of level or higher.
# Don't log private authentication messages!
*.info:mail:none:news:none:authpriv:none:cron:none /var/log/messages
# The authpriv file has restricted access.
authpriv.* /var/log/secure
# Log all the mail messages in one place.
mail.* /var/log/mailog
# Log cron stuff
cron.* /var/log/cron
# Everybody gets emergency messages
*.emerg *
# Save news errors of level crit and higher in a special file.
uucp,news.crit /var/log/spoller
# Save boot messages also to boot.log
local7.* /var/log/boot.log
#
# INN
#
news.-crit /var/log/news/news.crit
news.-err /var/log/news/news.err
news.notice /var/log/news/news.notice
```