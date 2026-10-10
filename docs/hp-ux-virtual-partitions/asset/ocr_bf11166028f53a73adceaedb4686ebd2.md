Note the LAN interface for the first vPar is *lan0* and the second is *lan1*. There are two LAN interfaces in this server, and even though they are separate vPar and instances of HP-UX, two different LAN interface names are required for the server to discern one interface from the other; as we'll see in the upcoming `netconf` files.

Host-related information is stored in `/etc/rc.config.d/netconf`. The following listing shows information related to *cvhdcn3* and again has no mention of the vPar name *cable1*:

# netconf* on host *cvhdcn3* (vPar *cable1*)

```
# cat /etc/rc.config.d/netconf
#
# netconf: configuration values for core networking subsystem
#
# @(#)B.11.11_LR $Revision: 1.6:119.6 $ Date: 97/09/10 15:56:01 $
#
# HOSTNAME:              Name of your system for uname -s and hostname
# OPERATING_SYSTEM:       Name of operating system returned by uname -s
#                        ---- DO NOT CHANGE THIS VALUE ----
#
# LOOPBACK_ADDRESS:      Loopback address
#                        ---- DO NOT CHANGE THIS VALUE ----
#
# IMPORTANT:  for 9.x-to-10.0 transition, do not put blank lines between
#  the next set of statements

HOSTNAME="cvhdcn3"
OPERATING_SYSTEM=HP-UX
LOOPBACK_ADDRESS=127.0.0.1

# Internet configuration parameters.  See ifconfig(Im), autopush(IIm)
#
# INTERFACE_NAME:  Network interface name (see lanscan(lm))
# IP_ADDRESS:      Hostname (in /etc/hosts) or IP address in decimal-dot
```