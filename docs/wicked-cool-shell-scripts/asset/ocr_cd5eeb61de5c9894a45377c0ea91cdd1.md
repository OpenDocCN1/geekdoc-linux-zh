including TCP, UDP, IPv4/v6, ICMP, IPsec, and more. Most of those protocols are irrelevant for a typical configuration; usually the protocol you want to examine is TCP. This script analyzes TCP protocol traffic, determining the percentage of packet transmission failure and including a warning if any values are out of bounds.

Analyzing network performance as a snapshot of long-term performance is useful, but a much better way to analyze data is with trends. If your system regularly has 1.5 percent packet loss in transmission, and in the last three days the rate has jumped up to 7.8 percent, a problem is brewing and needs to be analyzed in more detail.

As a result, this script is two parts. The first part, shown in Listing 10-10, is a short script that is intended to run every 10 to 30 minutes, recording key statistics in a log file. The second script (Listing 10-11) parses the log file, reporting typical performance and any anomalies or other values that are increasing over time.

> WARNING
> Some flavors of Unix can't run this code as is (though we've confirmed it's working on OS X as is)! It turns out that there is quite a variation in the output format (many subtle whitespace changes or slight spelling) of the netstat command between Linux and Unix versions. Normalizing netstat output would be a nice script unto itself.

# The Code

```
#!/bin/bash
# getstats--Every 'n' minutes, grabs netstats values (via crontab)

logfile="/Users/taylor/.netstatlog"  # Change for your configuration.
temp="/tmp/getstats.$$tmp"

trap "$(which rm) -f $temp" 0

if [ ! -e $logfile ] ; then      # First time run?
    touch $logfile
fi
( netstat -s -p tcp > $temp

# Check your log file the first time this is run: some versions of netstat
# report more than one line, which is why the "| head -1" is used here.
sent="$(grep 'packets sent' $temp | cut -d\ -f1 | sed \
's/[\'\digit:]/[\'\digit:]/g' | head -1)"
resent="$(grep 'retransmitted' $temp | cut -d\ -f1 | sed \
's/[\'\digit:]/[\'\digit:]/g')"
received="$(grep 'packets received' $temp | cut -d\ -f1 | \
sed 's/[\'\digit:]/[\'\digit:]/g')"
dupacks="$(grep 'duplicate acks' $temp | cut -d\ -f1 | \
sed 's/[\'\digit:]/[\'\digit:]/g')"
outoforders="$(grep 'out-of-order packets' $temp | cut -d\ -f1 | \
sed 's/[\'\digit:]/[\'\digit:]/g')"
connectreq="$(grep 'connection requests' $temp | cut -d\ -f1 | \
sed 's/[\'\digit:]/[\'\digit:]/g')"
```