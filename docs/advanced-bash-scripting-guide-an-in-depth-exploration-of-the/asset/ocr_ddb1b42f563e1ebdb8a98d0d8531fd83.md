# Advanced Bash-Scripting Guide

size
The size [/path/to/binary] command gives the segment sizes of a binary executable or archive file.
This is mainly of use to programmers.

```
bash$ size /bin/bash
text data bss dec hex filename
495971 22496 17392 535859 82d33 /bin/bash
```

# System Logs

logger
Appends a user-generated message to the system log (/var/log/messages). You do not have to
root to invoke logger.

```
logger Experiencing instability in network connection at 23:10, 05/21.
# Now, do a 'tail /var/log/messages'
By embedding a logger in a script, it is possible to write debugging information to
/var/log/messages.

logger -t $0 -i Logging at line "$LINENO"
# The "-t" option specifies the tag for the logger entry.
# The "-i" option records the process ID.

# tail /var/log/message
#
# Jul 7 20:48:58 localhost ./test.sh[1712]: Logging at line 3
```

logrotate
This utility manages the system log files, rotating, compressing, deleting, and/or mailing them, asnappropriate. It keeps the /var/log from getting cluttered with old log files. Usually cron runs
logrotate on a daily basis.

Adding an appropriate entry to /etc/logrotate.conf makes it possible to manage personal log
files, as well as system-wide ones.

> Stefano Falsetto created rotlog, which he considers to be an improved version of
logrotate.

# System Control

ps
ps Statistics: lists currently executing processes by owner and PID (process ID). This is usually
invoked with ax or options, which may be piped to grep or sed to search for a specific process (see
Example 15-14 and Example 29-3).

```
bash$ ps ax | grep sendmail
295 ? S 0:00 sendmail: accepting connections on port 25
```

To display processes in graphical "tree" format: ps afjx or ps ax --forest.

pgrep kill
Combining the ps command with grep or kill

Chapter 17. System and Administrative Commands