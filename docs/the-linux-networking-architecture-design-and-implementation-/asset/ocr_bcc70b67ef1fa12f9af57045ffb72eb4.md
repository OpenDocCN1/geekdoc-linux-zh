# 560 Appendix B Debugging in the Linux Kernel

Processing messages: There are various ways to store and to deliver messages which can be configured depending on the priority and origin of messages. The file /etc/syslog.conf always defines actions to be done in the following syntax:
origin.priority{origin.priority} action*

Each line outputs a processing rule, consisting of a sequence of message types (origin.priority), separated by a semicolon, and an action. Both the origin and the priority of a message type can be replaced by a wildcard (*). The following actions are possible:

+   The message can be written to a file. To write a message we state the file name with the absolute path (starts always with a "
The message can be sent to one or several users. The user names (login names) have to be stated in a list (separated by commas). The message is displayed only for those users who are logged in at the time of the event. You can use a wildcard (*) to send a message to all users logged in.
The message can be sent to the syslog daemon of another computer. which is specified with a leading "at" character (e.g., @tux.icsi.Berkeley.edu).

Example for a syslog configuration file—comments begin with #:

```
# /etc/syslog.conf — Configuration file for syslogd(8)
#
# print most on tty10
kern.warn;*err;authpriv.none /dev/tty10
*.emerg
#
# all email messages in one file
mail.* -var/log/mail
#
# all news messages
news.crit -var/log/news/news.crit
news.err -var/log/news/news.err
news.notice -var/log/news/news.notice
# enable this, if you want to keep all news messages
# in one file
news.* -var/log/news.all
# Warnings Warnings in one file
*.warn -var/log/warn
# save the rest in one file
**:mail.none;news.none -var/log/messages
# All messages with priority emerg and higher will be sent to the
# users, who are logged in. They will also be sent to syslog on
# host tux.icsi.Berkeley.edu.
*.emerg * With*
```