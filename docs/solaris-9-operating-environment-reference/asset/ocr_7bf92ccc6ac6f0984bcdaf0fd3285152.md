# 1392

# telnet

New!

open [-1 user [!] @hop1[@hop2...]@host [port]

Open a connection to the named host. If you specify no port number, telnet tries to contact a TELNET server at the default port. You can specify the host either as a host (see hosts(4), ipnodes(4)), or as an Internet address specified in the dot notation (see inet(TP), or inet6(7P)). If you specify the host as @hop1@hop2@host, the connection goes through hosts hop1 and hop2, using loose source routing to end host. The @ symbol is required as a separator between the hosts specified. If you use a len ! with IPv4, the connection follows strict source routing.

The -1 option passes to the remote system the user as the value of the ENVIRONMENT USER. The hop operands are new in the Solaris 8 release.

quit Same as close.

send arguments one or more special character sequences to the remote host. You can specify one or more of the following arguments:

+   abort Send the ABORT (abort process) sequence.

+   ao Send the AO (abort output) sequence to flush all output from the remote system to your terminal.

+   ayt Send the AYT (are you there) sequence. The remote system may may or not respond.

+   brk or break Send the BRK (break) sequence, which may have significance to the remote system.

+   do option dont option vont option Send the indicated protocol option negotiation. option can be the text name of the protocol or the option number corresponding to the option. The command is silently ignored if the indicated option negotiation is not valid in the current state. If you specify the help or ? option, list known option names. This command is useful for unusual debugging situations.

+   ec Send the EC (erase character) sequence to erase the last character entered.

+   el Send the EL (erase line) sequence to erase the line currently being entered on the remote system.

+   eof Send the EOF (end-of-file) sequence.

+   eor Send the EOF (end-of-record) sequence.

+   escape Send the current telnet escape character (initially ^]).

+   ga Send the GA (go ahead) sequence, which probably has no significance for the remote system.