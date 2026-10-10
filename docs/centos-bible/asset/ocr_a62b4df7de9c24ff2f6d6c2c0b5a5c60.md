configure rsyslogd to record varying levels of detail in the log files. It can be told to ignore all but the most critical message, or it can record every detail.

The rsyslogd daemon can even accept messages from other computers on your network. This is particularly handy because it enables you to centralize the management and reviewing of the log files from many systems on your network. There is also a major security benefit to this practice. If a system on your network is broken into, the cracker cannot delete or modify the log files because those files are stored on a separate computer.

It is important to remember, however, that those log messages are not, by default, encrypted. Anyone tapping into your local network will be able to eavesdrop on those messages as they pass from one machine to another. Also, although the cracker may not be able to change old log messages, she will be able to affect the system such that any new log messages should not be trusted.

It is not uncommon to run a dedicated loghost, a computer that serves no other purpose than to record log messages from other computers on the network. Because this system runs no other services, it is less likely that it will be broken into. This makes it nearly impossible for the cracker to erase her tracks. It does not, however, mean that all of the log messages are accurate after a cracker has broken into a machine on your network.

# ## Re-Directing Logs to a loghost with rsyslogd

To re-direct your computer's log files to another computer's rsyslogd, you must make some changes to your local rsyslogd's configuration file. The file that you need to work with is /etc/rsyslog.conf. If you are not already root, become root and then open the /etc/rsyslog.conf file in a text editor (such as vi). You should see something similar to this:

```
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
```