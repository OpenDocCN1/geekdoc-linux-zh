# Logging NSD/Unbound

which sends all debugging messages up to level 3 to that particular channel. Other lines in the channel definition specify the destination of those debugging messages. The higher the severity level, the more information is logged.

Watching the logs or the debugging output illustrates how DNS is misconfigured in the real world. That pesky dot at the end of names (or the lack thereof) accounts for an alarming amount of DNS traffic. The dot is at the end of each fully qualified domain name.

# Logging in NSD/Unbound

Logging in NSD and Unbound is simple in comparison to BIND. According to NSD's doc/README, "DNS doesn't do any logging." What really means is that NSD does not do any DNS traffic logging or monitoring; however, it does log important events to syslog.

By default, logs go to standard error and to syslog with facility daemon. However, if the logfile attribute of the server statement in either unbound.conf or nsd.conf is set, then logging goes to the specified file.

The amount of data logged (aside from errors, which are always included) is controlled by a verbosity level you set in the config files. In the case of unbound, you can also set the verbosity level as a command-line option. Verbosity varies from 0–5; the default levels are 0 for nsd and for unbound.

It can be a bit hard to get a handle on what the various verbosity levels mean for nsd. They may show syslog severity as follows:

+   - Level 3 - syslog severity "error"
- Level 4 - syslog severity "warning"
- Level 5 - syslog severity "notice"
- Level 6 - syslog severity "info"

The meanings of the levels for unbound are documented in the config file's page as follows:

+   - Level 0 – no information logged, only errors
- Level 1 – operational information
- Level 2 – detailed operational information
- Level 3 – query-level information on a per-query basis
- Level 4 – algorithm-level information
- Level 5 – cache misses and client identification

You can invoke nsd with the -d flag to turn on debugging mode. In this mode, nsd stays in the foreground instead of forking and exiting. This behavior is equivalent to what you get if you set debug-mode: yes in the server clause of nsd.conf. If you recompile nsd with DEBUG defined to a particular level, even debugging information becomes available, but it's mostly of value to developers.