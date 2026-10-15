The Linux kernel used in this firewall, v1.3.68, is relatively new. It will have to prove itself in the long run, but it looks promising.

The hardest part of building a good firewall lies in building good packet rules. Careful analysis is important to building good rules, but the ultimate proof is thorough testing. Test these rules, test them again, and then test them some more.

One good test strategy is to probe your firewall using SATAN running on some Internet host. I cannot stress this enough — the heart of your security lies in the rules you specify for your firewall. The rules given here work for me, but that doesn’t mean they’ll give you a secure installation. I would never presume that they are completely watertight. If you use these rules verbatim, be warned: you do so at your own risk.

This caution isn’t meant to be intimidating; I simply want to make it clear to you that constructing comprehensive and effective rules is not a trivial task.

# Listing 12.10 (continued)

```
if [ -f $MODDIR/slip.o ]; then
echo -n "slip"
/sbin/insmod $MODDIR/slip.o
fi
# And finally, start the diald
if [ -x /etc/ppp/diald.start ]; then
echo "starting diald"
/etc/ppp/diald.start
fi
echo "Done"
```

# Listing 12.11 A sample process listing from an active firewall.

```
scarab/etc/rc.d# ps -ax
PID TTY STAT TIME COMMAND
1 ? S 0:01 init [5]
2 ? SWN 0:00 (kflushd)
3 ? SWN 0:00 (kswapd)
9 ? S 0:05 update (bdflush)
30 ? S 0:00 /usr/sbin/cron -l10
43 ? S 0:00 /usr/sbin/syslogd
45 ? S 0:00 /usr/sbin/klogd
97 ? S 0:02 /usr/sbin/syslogd -m ppp mtu 1500 local 194.109.13.150
remote 0.0.0.0 dynamic connect /usr/sbin/chat -f
593 ? S 0:00 /sbin/getty -m 160 38400 ttyS0 vt100
603 ppp S 0:00 sh
610 ppr R N 0:00 ps -ax
528 ppp S N 0:00 -bash
scarab/etc/rc.0#
```