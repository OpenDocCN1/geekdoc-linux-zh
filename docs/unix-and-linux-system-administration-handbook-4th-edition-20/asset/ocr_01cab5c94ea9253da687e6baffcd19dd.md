# Alternatives to syslog

# Local authorization messages, e.g., sudo and npasswd
local2.debug /var/log/sudo.log
local2.alert /var/log/sudo-errs.log
auth.info /var/log/auth.log

# Other local stuff
local0.info /var/adm/nbl.log
local4.notice /var/admlog/da.log
local6.debug /var/adm/annex-isn.log
local7.debug /var/admlog/tcp.log

# Local messages (the default if no facility is specified)
user.info /var/admlog/user.log

Messages arriving from local programs and syslogs on the network are written to log files. In some cases, the output from each facility is put into its own file.

The central logging host generates the time stamp for each message as it writes the message out. The time stamps do not reflect the time on the originating host. If you have machines in several time zones or your system clocks are not synchronized, the time stamps are somewhat misleading.

# Syslog debugging

The logger command is useful for submitting log entries from scripts. You can also use it to test changes in syslog's configuration file. For example, if you have added the line

```
local5.warning /tmp/evi.log
```

and to verify that it is working, run

```
hp-ux$ logger -p local5.warning "test message"
```

A line containing "test message" should be written to /tmp/evi.log. If this doesn't happen, perhaps you forgot to create the evi.log file, to give the appropriate permissions, or to send syslog a hangup signal. Or you've used spaces instead of tabs?

# Alternatives to syslog

Although syslog has long been developed the reigning logging system for UNIX and Linux, several alternatives have been developed in an attempt to address some of syslog's shortcomings. One of these, syslog-ng (syslog, next generation), is now used by SUSE systems by default. From a configuration standpoint it is quite different from the standard syslog, and we do not describe it in this detail. It's available from balabit.com if you would like to try it on a non-SUSE system.

Syslog-ng adds additional configuration facilities, filtering based on message content, integrity, and better support for firewall restrictions when messages are forwarded over the network.