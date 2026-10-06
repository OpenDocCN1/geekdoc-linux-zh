Synchronizing Time

# Synchronizing Time

Red Hat Linux provides two ways to synchronize system time:

+   - rdate, which synchronizes to the clock of another host
- xntp, which synchronizes to Universal Coordinated Time (UTC)

The rdate program, contained in the rdate package, is the older and less sophisticated method of synchronizing time. To synchronize the local host's clock to that of another system, issue a command in the form

```
rdate -p -s host
```

where host is the name of the remote host. Common, a command such as this is placed in the /etc/rc.d/rc.local file, that will be executed when the system boots. Once synchronized, the clocks are apt to drift apart; the rdate command makes no provision for continual synchronization.
xntp program, which is contained in the xntp package, continually synchronizes the system clock to a precise estimate of UTC, based on time data obtained from remote servers. You can configure the cron service to regularly run ntptdate, another program in the xntp package; when invoked, ntptdate adjusts the system clock and terminates. Both xntp and ntptdate use the Network Time Protocol (NTP), described in RFC 1305. Typically, a host is configured to synchronize with multiple hosts, so that synchronization can continue even a host cannot be contacted.

NTP hosts are arranged in a hierarchy. Servers at the higher of the hierarchy—stratum 1—receive time information from a highly accurate, terrestrial source, such as radio signals from an atomic clock. Servers in stratum 2 synchronize to one or more stratum 1 servers, and so on.
TP continually adjusts the system time, usually to millisecond precision.
TP never adjusts the clock backward; if necessary, it slows the clock until real time catches up with the errant clock.

The man pages for ntptdate, the primary NTP programs are absent in some releases of the xntp package. Here's a man for ntptdate:

+   - ntptdate - set the date and time via NTP
SYNOPSIS
tptdate [ -bodos ] [ -a key# ] [ -e auth ] [ -k keyfile ] [ - samples ] [ - timeout ] server ...
DESCRIPTION
tptdate sets the local date and time by polling the Network

Copyright©2000 SYSEX, Inc., Alameda, CA www.sysex.com