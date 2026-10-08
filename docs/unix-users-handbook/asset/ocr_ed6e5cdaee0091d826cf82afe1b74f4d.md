the terminal by the local telnet before being transmitted to the remote host. In remote echo, any echoing of user input is done by the remote host. Applications that handle echoing of user input themselves, such as C shell, Korn shell, and vi (see csh(1), ksh(1), and vi(1)), do not work correctly with local echo.

options
Toggle viewing of TELNET options processing. When options viewing is enabled, all TELNET option negotiations are displayed. Options sent by telnet are displayed as "SENT", while options received from the TELNET server are displayed as "RCVD". The initial value for this toggle is FALSE.

netdata
Toggles the display of all network data (in hexadecimal format). The initial value for this toggle is FALSE.

?
Displays the legal toggle commands.

# RETURN VALUE

In the event of an error, or if the TELNET connection is closed by the remote host, telnet returns a value of 1. Otherwise it returns zero (0).

# DIAGNOSTICS

Diagnostic messages displayed by telnet are displayed below. Kerberos specific errors are listed in sis(5).

telnet/tcp: Unknown service
telnet was unable to find the TELNET service entry in the services(4) database.

hostname: Unknown host
telnet was unable to map the host name to an Internet address. Your next step should be to contact the system administrator to check whether there is an entry for the remote host in the hosts database (see hosts(4)).

?Invalid command
An invalid command was typed in telnet command mode.

system call> : ...
An error occurred in the specified system call. See the appropriate manual entry for a description of the error.

# AUTHOR

telnet was developed by the University of California, Berkeley.

# SEE ALSO

csh(1), ksh(1), login(1), rlogin(1), stty(1), telnetd(1M), hosts(4), services(4), termio(7), sis(5).