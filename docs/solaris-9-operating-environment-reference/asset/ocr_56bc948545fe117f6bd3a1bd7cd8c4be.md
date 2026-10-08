# telnet 1397

options Toggle the display of some internal TELNET protocol processing (having to do with telnet options). The initial value is false.

outbinary Enable or disable the BINARY option on output.

prettydump When the netdata toggle is enabled, prettydump is enabled, format the output from the netdata command in a more user-readable format. Put spaces between each character in the output. The beginning of any TELNET escape sequence is preceded by an asterisk (*) to aid in locating it.

skiprc When true, skip the reading of the .telnetrc file in your home directory when connections are opened. The initial value is false.

termdata Toggle the display of all terminal data (in hexadecimal format). The initial value is false.

? Display the legal toggle commands.

status Show the current status of telnet, including the peer you are connected to and the current mode.

z Suspend telnet. This command works only when you are using a shell that supports job control, as sh(1).

? [command] Get help. With no arguments, print a help summary. If you specify command, print the help information just for that command.

# Files

$HOME/.telnetrc

Commands to be executed before a telnet session is initiated.

/etc/nologin

Message displayed to users trying to log in during system shutdown.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |

| Availability | SUMcu |

# See Also

login(1), sh(1), stty(1), hosts(4), ipnodes(4), login(4), telnetrc(4), Nwm attributes(5), inet(7P), inet6(7P)