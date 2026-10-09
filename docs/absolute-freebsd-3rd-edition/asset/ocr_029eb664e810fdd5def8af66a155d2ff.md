log server on a network that had no uucp services.

# ## Logging by Program Name

If you’re out of facilities, you can use the program’s name as a matching term. An entry for a name requires two lines: the first line contains the program name with a leading exclamation mark and the second line sets up logging. For example, FreeBSD uses this to log ppp(8) information:

```
`!ppp  
`.*  
/var/log/ppp.log`
```

The first line specifies the program name and the second one uses wildcards to tell syslogd(8) to append absolutely everything to a file.

The !programname syntax affects all lines after it, so you must put it last in syslogd.conf. You can safely use it in an /etc/syslog.d file without worrying about affecting other entries.

# ## Logging to User Sessions

When you log to a user, any messages that arrive appear on that user’s screen. To log to a user session, list usernames separated by commas as the destination. To write a message to all users’ terminals, use an asterisk (*). For example, the default syslog.conf includes this line:

```
`*.emerg  *
`
```

This says that any message of emergency level will appear on all users’ terminals. Since these messages usually say “goodbye” in one way or another, that’s appropriate.

# ## Sending Log Messages to Programs

To direct log messages to a program, use a pipe symbol (|):

```
`mail.*  |/usr/local/bin/mailstats.pl`
```

# ## Logging to a Logging Host