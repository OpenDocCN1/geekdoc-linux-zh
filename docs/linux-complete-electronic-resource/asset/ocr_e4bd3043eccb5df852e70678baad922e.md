This is because the /etc/ppp/ip-up is executed for every PPP connection that comes up, so you need to carefully execute the correct routing commands for the particular link that comes up-and not when any other link comes up!

# Handling E-mail Queues

When the link between two LANs comes up, you may well want to make sure that e-mail that is queued at either end is flushed-sent out to its destination. This is done by adding the appropriate sendmail invocation.

Using the bash case statement on an appropriate parameter that pppd passes into the script accomplishes this. For example, this is the /etc/ppp/ip-up script I use to handle our WAN links and the link to my home Ethernet (also handled on the same PPP server).

# A Sample /etc/ppp/ip-up Script

The following example provides a variety of example uses.

```
#!/bin/bash

# Script which handles the routing issues as necessary for pppd
# Only the link to Newman requires this handling.
#
# When the ppp link comes up, this script is called with the
# following parameters
# $1 the interface name used by pppd (e.g. ppp3)
# $2 the tty device name
# $3 the tty device speed
# $4 the local IP address for the interface
# $5 the remote IP address
# $6 the parameter specified by the 'ipparam' option to pppd

case "$5" in
# Handle the routing to the Newman Campus server
        202.12.126.1)
	    /sbin/route add -net 202.12.126.0 gw 202.12.126.1
        # and flush the mail queue to get their email there asap!
        /usr/sbin/sendmail -q &
        ;;
        139.130.177.2)
# Our Internet link
        # When the link comes up, start the time server and synchronise
        # to the world provided it is not already running
```