# LISTING 13.2  CONTINUED

```
lrwxrwxrwx  1 root  root  16 Feb  4 16:17 K40rstatd -> ../init.d/rstatd*
lrwxrwxrwx  1 root  root  15 Feb 15 14:11 K44dhcpd -> ../init.d/dhcpd*
lrwxrwxrwx  1 root  root  17 Feb  9 19:32 K47rusersd -> ../init.d/rusersd*
lrwxrwxrwx  1 root  root  18 Feb  9 19:32 K48rwhod -> ../init.d/rwhod*
lrwxrwxrwx  1 root  root  15 Feb  4 16:17 K50mta -> ../init.d/mta*
lrwxrwxrwx  1 root  root  15 Feb  9 21:54 K55ldap -> ../init.d/ldap*
lrwxrwxrwx  1 root  root  15 Feb  9 20:46 K55snmpd -> ../init.d/snmpd*
lrwxrwxrwx  1 root  root  15 Feb  9 19:42 K60nfs -> ../init.d/nfs*
lrwxrwxrwx  1 root  root  15 Feb  9 19:47 K70ntp -> ../init.d/ntp*
lrwxrwxrwx  1 root  root  17 Feb  4 16:17 K73ipxipd -> ../init.d/ipxipd*
lrwxrwxrwx  1 root  root  20 Feb 15 13:46 K79nis-client -> ../init.d/
➜nis-client*
lrwxrwxrwx  1 root  root  20 Feb 15 13:46 K80nis-server -> ../init.d/
➜nis-server*
lrwxrwxrwx  1 root  root  14 Feb  9 19:32 K84inet -> ../init.d/inet*
lrwxrwxrwx  1 root  root  17 Feb  9 19:42 K85portmap -> ../init.d/portmap*
lrwxrwxrwx  1 root  root  15 Feb  9 21:53 K90named -> ../init.d/named*
lrwxrwxrwx  1 root  root  20 Feb  9 21:17 K96irda-utils -> ../init.d/
➜irda-utils*
lrwxrwxrwx  1 root  root  17 Feb  9 19:30 S01network -> ../init.d/network*
lrwxrwxrwx  1 root  root  16 Feb  9 19:30 S05syslog -> ../init.d/syslog*
lrwxrwxrwx  1 root  root  17 Feb  9 19:30 S05urandom -> ../init.d/urandom*
lrwxrwxrwx  1 root  root  16 Feb  9 19:32 S06pcmcia -> ../init.d/pcmcia*
lrwxrwxrwx  1 root  root  18 Feb  9 19:30 S20netmount -> ../init.d/netmount*
lrwxrwxrwx  1 root  root  16 Feb  9 19:37 S26ipx -> ../init.d/ipx*
lrwxrwxrwx  1 root  root  15 Feb  9 20:04 S35ipsec -> ../init.d/ipsec*
lrwxrwxrwx  1 root  root  15 Feb  4 16:16 S35lpd -> ../init.d/lpd*
lrwxrwxrwx  1 root  root  14 Feb  9 19:46 S40cron -> ../init.d/cron*
lrwxrwxrwx  1 root  root  17 Feb  9 19:37 S75keytable -> ../init.d/keytable*
lrwxrwxrwx  1 root  root  15 Feb  9 19:30 S80local -> ../init.d/local*
lrwxrwxrwx  1 root  root  16 Feb  9 19:30 S99bigfs -> ../init.d/bigfs*
lrwxrwxrwx  1 root  root  20 Feb  9 19:30 S99rmmologin -> ../init.d/
➜rmmologin*
lrwxrwxrwx  1 root  root  17 Feb  9 19:30 S99skipped -> ../init.d/skipped*
lrwxrwxrwx  1 root  root  16 Feb  9 20:49 S99webmin -> ../init.d/webmin*
```

The files in the /etc/rc.d/rc#.d directories all begin with either an S or a K for start or kill, respectively, a number that indicates a relative order for the scripts, and the script name—commonly the same name as the master script to which it is linked (found in init.d). For example, you might see S35lpd. This is a symbolic link to /init.d/lpd and is used by rc to run the lpd script in init.d with the argument start, which starts up the line printer daemon. The scripts can also be called from the following command line:

```
/etc/rc.d/init.d/lpd start
```

The nice part about SysV initialization is that it is easy for root to start, stop, and, in many cases, restart or reload a daemon or process subsystem from the command line simply by calling the script in init.d with the appropriate argument.

When not called from a command line with an argument, the /etc/rc.d/rc script determines what to run, and how, based on the previous and current runlevel. For example, if you are in runlevel 3 and change to runlevel 2, the /etc/rc.d/rc script uses the runlevel command as you did earlier, and looks at the differences in the two directories corresponding to the two