# Local authorization messages, e.g., sudo and npasswd
local2.debug		/var/log/sudo.log
local2.alert		/var/log/sudo-errs.log
auth.info		/var/log/auth.log

# Other local stuff
local0.info		/var/adm/nbl.log
local4.notice		/var/adm/da.log
local6.debug		/var/adm/annx-isn.log
local7.debug		/var/adm/tcp.log

# Local messages (the default if no facility is specified)
user.info		/var/adm/user.log

Messages arriving from local programs and syslogds on the network are written to log files. In some cases, the output from each facility is put into its own file.

The central logging host generates the time stamp for each message as it writes the message out. The time stamps do not reflect the time on the originating host. If you have machines in several time zones or your system clocks are not synchronized, the time stamps can be somewhat misleading.

# Syslog debugging

The logger command is useful for submitting log entries from shell scripts. You can also use it to test changes in syslogd's configuration file. For example, if you have just added the line

```
local5.warning	/tmp/evi.log
```

and want to verify that it is working, run

```
hp-ux5$ logger -p local5.warning "test message"
```

A line containing "test message" should be written to /tmp/evi.log. If this doesn't happen, perhaps you forgot to create the evi.log file, to give the file appropriate permissions, or to send syslogd a hangup signal. Or perhaps you've used spaces instead of tabs?

# Alternatives to syslog

Although syslog has long been the reigning logging system for UNIX and Linux, several alternatives have been developed in an attempt to address some of syslog's shortcomings. One of these, syslog-ng (syslog, next generation), is now used on SUSE systems by default. From a configuration standpoint it is quite different from the standard syslog, and we do not describe it in detail in this book. It's available from balabit.com if you would like to try it on a non-SUSE system.

Syslog-ng adds additional configuration facilities, filtering based on message content, message integrity, and better support for firewall restrictions when messages are forwarded over the network.