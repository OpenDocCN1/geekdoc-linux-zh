# 1494

# uucp, uulog, uaname

# Examples

The following example shows four users are logged in to the system castle.

```
castle$ users
winsor ray des rob
castle%
```

# Files

```
/var/adm/utmpx
```

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNWscpu |

# See Also

who(1), attributes

# uucp, uulog, uaname — UNIX-to-UNIX System Copy

# Synopsis

```
/usr/bin/uucp [-c] [-C] -d [-f] [-grade] [-jmr] [-user] [-sfile] [-xdebug-level]
source-file destination-file
/usr/bin/uulog [-ssys] [-f system] [-x] [-number] system
/usr/bin/uaname [-c -1]
```

# Description

The uucp (UNIX-to-UNIX copy) suite of commands is part of a data communications subsystem that enables you to transfer ASCII and binary files between systems, execution of commands, queue jobs for later transfer, and automatically retry when transfer fails. The complete uucp suite of commands includes user commands and functions, security features, logging and debugging tools, and a number of data transfer protocols. This section describes the uucp, uulog, and uan commands.

# uucp

uucp copies files named by the source-file arguments to the location specified by the destination-file argument.

# uulog

uulog queries a log file of uucp or uuxqt transactions in file
/var/uucp/.Log/uucico/system or /var/uucp/.Log/uxxqt/system.

# uaname

uaname lists the names of systems known to uucp.