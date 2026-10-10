# 200 Chapter Eight

```
# Network services, Internet style
#
# Note that it is presently the policy of IANA to assign a
# single well-known port number for both TCP and UDP; hence,
# most entries here have two entries even if the protocol
# doesn't support UDP operations.
# Updated from RFC 1340, 'Assigned Numbers' (July 1992).
# Not all ports are included, only the more common ones.

tcpmux	1/tcp		# TCP port service multiplexer
echo	7/tcp
		7/udp
discard	9/tcp		sink null
		9/udp		sink null
systat	11/tcp		users
daytime	13/tcp
		13/udp
daytime	17/tcp
		17/udp
qotd		17/tcp		quote
msp		18/tcp		# message send protocol
		18/udp		# message send protocol
chargen	19/tcp		tystst source
		19/udp		tystst source
ftp-data	20/tcp
ftp		21/tcp
ssh		22/tcp		# SSH Remote Login Protocol
		22/udp		# SSH Remote Login Protocol
telnet	23/tcp
# 24 - private
smtpp	25/tcp		mail
# 26 - unassigned
time	37/tcp		timeserver
		37/udp		timeserver
		39/udp		resource	# resource location
nameserver	42/tcp		name	# IEN 116
whois	43/tcp		nicname
re-mail-ck	50/tcp		# Remote Mail Checking Protocol
		50/udp		# Remote Mail Checking Protocol
domain	53/tcp		nameserver	# name-domain server
		53/udp		nameserver
mtop	57/tcp		# deprecated
bootps	67/tcp		# BOOTP server
		67/udp
bootpc	68/tcp		# BOOTP client
```