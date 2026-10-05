# Chapter 17 DNS: The Domain Name System

limit nsd to a particular protocol, and port sets the network port on which to listen for incoming queries.

You should not normally need any of these options, the defaults are fine.

+   - identity: string [hostname]
hide-version: yes | no [no]

This pair of options controls whether nsd tells the truth about its version and hostname when queried for the CHAOS class names id.server and version.server. As explained on page 598, we recommend not tampering with these values.

+   - logfile: filename [stderr and syslog]
verbosity: level [0]
debug-mode: yes | no [no]
statistics: #secs [0] # statistics

Logging is, by default, to standard error and to syslog (facility daemon), with the amount of logging determined by the verbosity option. The range of possible values is 0–5; higher numbers mean more data should be logged. The logfile parameter directs log messages to a file instead of sending them to syslog.

If you specify debug-mode, nsd does not fork extra copies of itself and stays to your terminal that you can see messages to standard error.

If you keep statistics, #secs to the number of seconds between dumps. Statistics are like other log messages, they go to the log file or to syslog if no log file has been specified. It is best to watch the output for a bit to make sure you have chosen a sensible dumb interval and are not filling your disks with information.

+   - database: filename [/var/db/nsd/nsd.db]
diffile: filename [/var/db/nsd/xfrd.db]
xfrfile: filename [/var/db/nsd/xfrd.state]
pid-file: filename [Os-specific, usually /var/run/nsd.pid]
zondirect: directory [/etc]

Compiled zone files and zone transfer default logging to /var/db/nsd; it’s unlikely that you will need to change this. The PID file should show where operating system puts other PID files, usually in /var/run. By default, human-editable zone files go in /etc/nsd, which feels like a bad choice. Considering moving them /var, perhaps to /var/nsd/zones.

+   - tcp-count: int [10]
server-count: int [1]
xfrd-reload-timeout: #sec [10]

tcp-count limits the number of concurrent TCP connections the server can use for zone transfers. You’ll know you’ve exceeded the limit when you see “xfrd: max number of TCP connections (10) reached” in the log. If that happens frequently, you should increase this limit.