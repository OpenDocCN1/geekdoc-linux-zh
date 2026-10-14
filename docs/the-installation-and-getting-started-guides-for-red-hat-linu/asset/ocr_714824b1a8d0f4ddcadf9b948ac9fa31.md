free command displays the amounts of free and used memory on your system. The skill command sends a terminate command (or another specified signal) to a specified set of processes. The snice command is used to change the scheduling priority of specified processes. The tload command prints a graph of the current system load average to a specified tty. The uptime command displays the current time, how long the system has been running, how many users are logged on and system load averages for the past one, five and fifteen minutes. The w command displays a list of the users who are currently logged on and what they're running. The watch program watches a running program. The vmstat command displays virtual memory statistics about processes, memory, paging, block I/O, traps and CPU activity.

# procps-X11 — (Version 2.0.2, 0K)

The procps-X11 package contains the XConsole shell script, a backwards compatibility wrapper for the xconsole program.

# psacct — (Version 6.3, 87K)

The psacct package contains several utilities for monitoring process activities, including ac, lastcomm, acct on and sa. The ac command displays statistics about how long users have been logged on. The lastcomm command displays information about previous executed commands. The acton command turns process accounting on or off. The sa command summarizes information about previously executed commands. Install the psacct package if you'd like to use its utilities for monitoring process activities on your system.

# psmisc — (Version 18, 46K)

[B]

The psmisc package contains utilities for managing processes on your system: pstree, killall and fuser. The pstree command displays a tree structure of all of the running processes on your system. The killall command sends a specified signal (SIGTERM if nothing is specified) to processes identified by name. The fuser command identifies the PIDs of processes that are using specified files or filesystems.

# rdate — (Version 0.960923, 5K)

[W][S]

The rdate utility retrieves the date and time from another machine on your network, using the protocol described in RFC 868. If you run rdate as root, it will set your machine's local time to the time of the machine that you queried. Note that rdate isn't scrupulously accurate. If you are worried about milliseconds, get the ntpd program instead.