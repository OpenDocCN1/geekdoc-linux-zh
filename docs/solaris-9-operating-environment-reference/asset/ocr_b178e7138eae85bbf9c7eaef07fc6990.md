# 1168

# login

-l username

Specify a different username for the remote login. If you do not use this option, the remote username used is the same as your local username.

-L Run the login session in printout mode.

# Escape Sequences

Lines that you type with the tilde character are escape sequences (you can change the escape character with the -e option).

~ Disconnect from the remote host. This action is not the same as a logout because the local host breaks the connection with no warning to the remote end.

~susp suspend the login session (only if you are using a shell with job control). susp is your suspend character, see tty(1).

~dsusp suspend the input half of login, but output is still seen (only if you are using a shell with job control). dsusp is your "deferred suspend" usually Control-Y; see tty(1).

# Operands

hostname The name of the remote system on which login establishes the remote login session.

# Files

/etc/passwd Contains information about users' accounts.

/etc/hosts Hosts database for IPv4 hosts. Starting with the Solaris 8 release, it's also a symbolic link to /etc/inet/hosts.

/etc/equiv List of trusted host names with shared user names.

/etc/inet/ipnodes Hosts database for IPv6 hosts. New in the Solaris 8 release.

/etc/nologin Message displayed to users attempting to log in during system shutdown.

$HOME/.hosts Private list of trusted hostname/username combinations.

/usr/hosts/* For host-name version of the command.