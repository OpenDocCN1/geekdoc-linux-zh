
which sends all debugging messages up to level 3 to that particular channel. Other lines in the channel definition specify the destination of those debugging messages. The higher the severity level, the more information is logged.

Watching the logs or the debugging output illustrates how often DNS is misconfigured in the real world. That pesky little dot at the end of names (or rather, the lack thereof) accounts for an alarming amount of DNS traffic. The dot is required at the end of each fully qualified domain name.

## Logging in NSD/Unbound

Logging in NSD and Unbound is simple in comparison to BIND. According to NSD’s **doc/README** file, “NSD doesn’t do any logging.” What that really means is that NSD does not do any DNS traffic logging or monitoring; however, it does log important software events to syslog.

By default, log messages go to standard error and to syslog with facility daemon. However, if the logfile attribute of the server statement in either **unbound.conf** or **nsd.conf** is set, then logging goes to the specified file.

The amount of data logged (aside from errors, which are always included) is controlled by a verbosity level that you set in the config files. In the case of **unbound**, you can also set the verbosity level as a command-line option. Verbosity varies from 0–5; the default levels are 0 for **nsd** and 1 for **unbound**.

It can be a bit hard to get a handle on what the various verbosity levels mean for **nsd**. They map to syslog roughly as follows:

- Level 3 – syslog severity “error”
- Level 4 – syslog severity “warning”
- Level 5 – syslog severity “notice”
- Level 6 – syslog severity “info”

The meanings of the levels for **unbound** are documented in the config file’s man page as follows:

- Level 0 – no information logged, only errors
- Level 1 – operational information
- Level 2 – detailed operational information
- Level 3 – query-level information on a per-query basis
- Level 4 – algorithm-level information
- Level 5 – cache misses and client identification

You can invoke **nsd** with the **-d** flag to turn on debugging mode. In this mode, **nsd** stays in the foreground instead of forking and exiting. This behavior is equivalent to what you get if you set debug-mode: yes in the server clause of **nsd.conf**. If you recompile **nsd** with DEBUG defined to a particular level, even more debugging information becomes available, but it’s mostly of value to developers.

unbound also has a -d flag to turn on debugging mode. You can boost the verbosity of the debugging information with the -v flag; for more, try -v -v. Debugging output is separate from the verbosity of logging information set in the config file. You can configure additional logging to help debug DNSSEC signature validation issues; see page 666.

## Name server control programs

All three of our name servers come with a control program: nsdc controls nsd, rndc controls named, and unbound-control controls unbound. nsdc works on the local machine only, but rndc and unbound-control can work across the Internet if you set them up that way.

rndc uses a network socket to communicate with named and uses TSIG authentication for security. unbound-control uses SSL/TLS, and nsdc uses signals.

Using BIND’s rndc

Table 17.16 shows some of the options accepted by rndc. Typing rndc with no arguments gives a list of available commands and a short description of what they do. Earlier incarnations of rndc used signals as nsdc does, but with over 25 commands, the BIND folks ran out of signals long ago. Commands that produce files put them in whatever directory is specified as named’s home in named.conf.

rndc reload makes named reread its configuration file and reload zone files. The reload zone command is handy when only one zone has changed and you don’t want to reload all the zones, especially on a busy server. You can also specify a class and view to reload only the selected view of the zone’s data.

Note that rndc reload is not sufficient to add a completely new zone; that requires named to read both the named.conf file and the new zone file. For new zones, use rndc reconfig, which rereads the config file and loads any new zones without disturbing existing zones.

rndc freeze zone stops dynamic updates and reconciles the journal of dynamic updates to the data files. After freezing the zone, you can edit the zone data by hand. As long as the zone is frozen, dynamic updates are refused. Once you’ve finished editing, use rndc thaw zone to start accepting dynamic updates again.
