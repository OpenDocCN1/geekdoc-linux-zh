# 3.4.1.2. Administrative Tools

Administrative tools play an integral part in the management of a server.

named-checkconf

The named-checkconf program checks the syntax of a named.conf file.

named-checkconf [-directory] [filename]

named-checkzone

The named-checkzone program checks a master file for syntax and consistency.

named-checkzone [-dq] [-c class] zone [filename]

The remote name daemon (rndc) program allows the system administrator to control the operation of a nameserver. If you run rndc without any options it will display a usage message follows:

rndc [-c config] [-s server] [-p port] [-y key] command [command...]

command is one of the following:

reload

Reload configuration file and zones.

reload zone [class [view]]

Reload the given zone.

refresh zone [class [view]]

Schedule zone maintenance for the given zone.

reconfig

Reload the configuration file and load new zones, but not reload existing zone files even if they have changed. This is faster than a full reload when there is a large number of zones because it avoids the need to examine the modification times of the zones files.