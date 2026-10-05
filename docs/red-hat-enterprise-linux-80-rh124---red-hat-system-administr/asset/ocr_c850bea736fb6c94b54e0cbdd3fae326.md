# CHAPTER 2 Analyzing and Sorting Logs

Log messages sometimes match more than one rule in syslog.conf. In such cases, one message is stored in more than one log file. To limit messages stored, the key word none in the priority field identifies that no messages for the indicated facility should be stored in the given file.

Instead of logging syslog messages to a file, they can be printed to the terminals of all logged-users. The rsyslog.conf file has a setting to print all the syslog messages with the emerg priority to the terminals of all logged-in users.

# SAMPLE RULES OF RSYLOG

#### RULES ####

+   # Log all kernel messages to the console.
# Logging much elseutters up the screen.
#kern.*

+   # Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail;authpriv.none;cron.none

+   # The authpriv file has restricted access.
authpriv.*

+   # Log all the mail messages in one place.
mail.*

+   # Log cron stuff
cron.*

+   # Everybody gets emergency messages
*.emerg

+   # Save new errors of level crit and higher in a special file.
uucp,news.crit

+   # Save boot messages also to boot.log
local7.*

> NOTE
The syslog subsystem has many features beyond the scope of this course. For those who wish to explore further, consult the rsyslog.conf(5) man page and the extensive HTML documentation in /usr/share/doc/rsyslog/html/index.html contained in the rsyslog-doc package, available from the AppStream repository in Red Hat Linux 8.

# LOG FILE ROTATION

The logrotate tool rotates logs to keep them from taking too much space in the file system containing /var/log directory. When a log is rotated, it is renamed with an extension indicating the date it was rotated. For example, the old /var/log/messages file may

RH124-RHEL8.0-en-1-20190507 353