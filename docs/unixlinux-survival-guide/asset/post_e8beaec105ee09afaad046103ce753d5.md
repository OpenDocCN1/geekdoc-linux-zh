
out about the open ports on your systems or to render the services on your systems useless. This is called a DOS attack (pun intended), spelled out denial-of-service.

If an IDS system is active inside the network (see Chapter 7 for more on Intrusion Detection Systems), then such attempts should not go unnoticed. But beyond being a pointer that an attack is going on, the growth of connections in SYN state could also mean you have a malfunctioning device connected to your network, slowing down the established connections. The proper use of baselining statistics enables you to visualize these changes (the same holds true for connections in TIME_WAIT state) and react accordingly. So monitoring these counters is not only about defending yourself, but also about being notified of changes regarding the behavior of your networks, thus allowing you to make assumptions about the state of those networks.

Listing 3.13 demonstrates a script used to record the number of connections in the mentioned SYN states.

## LISTING 3.13 Recording the Number of Connections Regarding the SYN State

```
#!/usr/bin/perl
# $Id: base_syn.pl,v 1.1 2004/08/24 10:08:50 erikk Exp erikk $
##################################################
#
#    file:          base_syn.pl
#
#    purpose:       count number of network
#                   connections in SYN state
#
#    author:        Erik Keller
#
#    parameters:    -4   counts inet4
#                   -6   counts inet6
#                   -i   incoming connections
#                   -o   outgoing connections
#                   none counts all
#
##################################################

use Getopt::Std;

# Variables
# path and files !!!!! change for every system
$varpath="/export/home/users/erikk/work/baselines/var";
$thelogfile="base_syn.log";
```

```
# connection counter
$syn_conns = 0;

# check for options on cmdline
# netstat options work on Solaris and OS/X
# Linux needs -A <family>, check man-page
getopt('');
if($opt_4)
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
# check if all, incoming or outgoing
if($opt_i)
{
    # incoming
    $nstate = "SYN_RECEIVED";
}
elsif($opt_o)
{
    # outgoing
    $nstate = "SYN_SENT";
}
else
{
    $nstate = "SYN";
}

# open the input stream from netstat
open(MY_NETSTAT, "$netstatcmd |") or die "$0: couldn't run: $!";
while(<MY_NETSTAT>)
{
    chop;
    if(/$nstate/)
    {
        $syn_conns++;
    }
}
```

```
}

close(MY_NETSTAT);

# write to file
open(MY_LOG,">>$varpath/$thelogfile")
    or die "$0: couldn't open log file: $!";
print MY_LOG "$syn_conns\n";

close(MY_LOG);

# EOF
```

The script is able to record only the number of either incoming (option -i) or outgoing (option -o) connections if needed. There should not be a value greater than zero during normal operations.

## 3.1.11 Creating the Graphs

The numbers recorded in the log files are of limited use. Great deviations might become visible, but only if the deviation is big enough; it is almost impossible to spot evolving trends. To visualize data gathered by sar, you could use the program sag, but this program is far from user-friendly; sometimes it requires being run inside an x-term using a special Tektronix-emulation mode. The other issue here is the fact that it cannot be used to visualize the data recorded by the other scripts.

Taking this into account, two options remain: either you use a spreadsheet program (like OpenOffice Calc or MS Excel, for example) capable of transforming your columns of numbers into meaningful graphics, or you use the program gnuplot. The drawback of gnuplot—and the same goes for OpenOffice Calc—is that, with the exception of GNU-Linux and Solaris, the program needs to be obtained and installed first (to obtain gnuplot for other *NIX brands, you can use the Internet addresses in Appendix C of this book). The program is usually available as binary, ready to be installed and used; there is no need to compile it first.

There is no real need to explain the use of a spreadsheet program, but a couple of remarks regarding gnuplot are appropriate. The program is free software; it runs on almost all operating systems available and enables you to plot functions and—more interesting to the task at hand—data sets. The name has no connection whatsoever to GNU; in fact, pronounced correctly the name should sound like "newplot." If you are interested in the history of the program, then http://www.gnuplot.info/faq/faq.html is the place to learn more about how the program came to life.

After the program is installed on a system, it can be started by executing gnuplot on the command line. Listing 3.14 shows the result.
