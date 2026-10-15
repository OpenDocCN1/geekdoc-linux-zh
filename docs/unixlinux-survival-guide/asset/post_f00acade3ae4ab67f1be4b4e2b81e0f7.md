
```perl
@myrec = split(" ", $_);
$tcpoutsegs = $myrec[0];
}
if(/segments retransmited/)
{
@myrec = split(" ", $_);
$tcpretssegs = $myrec[0];
}
}

close(MY_NETSTAT);

# calculate ratio
$retransratio = (($tcpretssegs * 100)/$tcpoutsegs);

# write to file
open(MY_LOG, ">>$varpath/$thelogfile")
or die "$0: couldn't open log file: $!";
print MY_LOG "$retransratio\n";

close(MY_LOG);

# EOF
```

The GNU-Linux variant used (SuSE 8.2) allows you to filter the output of netstat for TCP statistics via the -t option. The resulting lines are searched for the strings segments send out and segments retransmited (that's not a misspelling) to obtain the values.

With these two scripts as a base, you should be able to customize as necessary and obtain the values needed for the calculation of the retransmission ratio on almost every machine.

### 3.1.9 What Does TIME_WAIT Mean?

A TCP network connection in the TIME_WAIT state signals that the connection was terminated and that the system will wait for a predefined span of time for incoming packets from the other system or, respectively, that it will wait for the connection partner to confirm the termination of the connection. The TCP protocol was designed this way to minimize the loss of packets.

So far so good—if the requested confirmation for the termination of the connection is not received within the predefined time span, the system will drop the connection anyway. Usually, this design choice doesn't pose a problem at all, but systems with a huge number of open connections, for example, a Web server, could tie up precious resources this way. Even worse, some clients using a TCP/IP stack of questionable quality might let the number of connections in TIME_WAIT state grow exponentially (even if this statement covers the better part of Windows, there are other systems showing the same behavior, too). Changes to the time-out value of TIME_WAIT should be executed with extreme care, though.

The script in Listing 3.12 enables you to obtain the number of connections in TIME_WAIT state (HP-UX sometimes uses a TIME_WAIT2 state as well).

**LISTING 3.12 Recording the Number of Connections in TIME_WAIT**

```perl
#!/usr/bin/perl
# $Id: base_timewait.pl,v 1.1 2004/08/24 09:02:03 erikk Exp erikk $
################################################################
#
#    file:          base_timewait.pl
#
#    purpose:       number of network connections
#                   in TIME_WAIT state
#
#    author:        Erik Keller
#
#    parameters:    -4    counts inet4
#                   -6    counts inet6
#                   none  counts all
#
################################################################

use Getopt::Std;

# Variables
# path and files !!!!!! change for every system
$varpath="/export/home/users/erikk/work/baselines/var";
$thelogfile="base_timewait.log";

# connection counter
$timewait_conns = 0;

# check for options on cmdline
# netstat options work on Solaris and OS/X
# Linux needs -A <family>, check man-page
getopt('');
if ($opt_4)
{
$netstatcmd = "netstat -f inet";
}
elsif($opt_6)
{
    $netstatcmd = "netstat -f inet6";
}
else
{
    $netstatcmd = "netstat";
}

# open the input stream from netstat
open(MY_NETSTAT, "$netstatcmd |") or die "$0: couldn't run: $!";
while(<MY_NETSTAT>)
{
    chop;
    if(/TIME_WAIT/)
    {
        $timewait_conns++;
    }
}

close(MY_NETSTAT);

# write to file
open(MY_LOG,">>$varpath/$thelogfile")
    or die "$0: couldn't open log file: $!";
print MY_LOG "$timewait_conns\n";

close(MY_LOG);

# EOF
```

The script resembles, more or less, the one used to count the active network connections. As already mentioned, if this script is needed for the purpose of the system to be monitored, it depends heavily on the intended use of that system.

### 3.1.10 Monitoring SYN Packets

The SYN_SENT and SYN_RECEIVED states of network connections translate into either the system trying to establish a connection (SYN_SENT) or another system trying to establish a connection to it (SYN_RECEIVED). This behavior is quite normal, but because not every system connected to the Internet is to be trusted, you should be aware of so-called SYN attacks. These attacks are used, among other things, to find
