When you define your host and networks, you can also decide what type of services you want on your network connection. These services are run through the `/etc/services` file. Most of the network services that run through here use only TCP; however, UNIX is also marked in the file.

Slackware Linux comes with all these services enabled. You might want to close down certain services if they're not being used. For example, you probably don't need port 1, port 7, port 11, or port 15. Because a lot of the ports on your system are unnecessary, you can turn them off by placing a # character to comment out that field. I would not delete it; you may need that service later on. Listing 11-2 shows the `/etc/services` file.

# Listing 11-2: The `/etc/services` file

```
# Network services, Internet style
#
# Note that it is presently the policy of IANA to assign a single well-known
# port number for both TCP and UDP; hence, most entries here have two entries
# even if the protocol doesn't support UDP operations.
# Updated from RFC 1340, "Assigned Numbers" (July 1992). Not all ports
# are included, only the more common ones.
#
# from: @(#)services 5.8 (Berkeley) 5/9/91
# $Id: services,v 1.9 1993/11/08 19:49:15 cgd Exp $
#
tcpx	p 1/tcp	p # TCP port service multiplexer
echo	p 7/tcp
 echo	p 7/udp
 discard	p 9/tcp	p sink null
discard	p 9/udp	p sink null
systat	p 11/tcp	p users
daytime	p 13/tcp
daytime	p 13/udp
netstat	p 15/tcp
qotd	p 17/tcp	p quote
mspp	p 18/tcp	p # message send protocol
mspp	p 18/udp	p # message send protocol
chargen	p 19/tcp	p ttyst source
chargen	p 19/udp	p ttyst source
ftp	p 21/tcp
# 22 - unassigned
telnet	p 23/tcp
# 24 - private
smtp	p 25/tcp	p mail
# 26 - unassigned
time	p 37/tcp	p timeserver
```