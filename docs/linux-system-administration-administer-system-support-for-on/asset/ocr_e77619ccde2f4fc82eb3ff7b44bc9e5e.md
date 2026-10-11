The alias is so you can type ssh oracle instead of ssh oracle.tigerlair.com.

```
#
# hosts	This file describes a number of hostname-to-address
#	mappings for the TCP/IP subsystem. It is mostly
#	used at boot time, when no name servers are running.
#	On small systems, this file can be used instead of a
#	"named" name server. Just add the names, addresses
#	and any aliases to this file...
#
# By the way, Arnt Gulbrandsen <agulbra@nvg.unit.no> says that 127.0.0.1
# should NEVER be named with the name of the machine. It causes problems
# for some (stupid) programs, irc and reputedly talk. :^)
#
# For loopbacking.
127.0.0.1 localhost
1.2.3.4	www.tigerlair.com tigerlair
2.3.4.5	oracle.tigerlair.com oracle

# End of hosts.
```

# The network Files

Respectively, Slackware defines networks in a similar fashion. The listings are reserved without any aliases:

```
networkname:networkaddress

/etc/networks
#
# networks	This file describes a number of netname-to-address
#	mappings for the TCP/IP subsystem. It is mostly
#	used at boot time, when no name servers are running.
#
loopback	127.0.0.0
localnet	1.1.1.0

# End of networks.
```