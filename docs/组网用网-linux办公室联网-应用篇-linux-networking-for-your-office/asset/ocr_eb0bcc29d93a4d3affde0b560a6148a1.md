# File Sharing

# PART III

If you see a process other than grep, then atalk is running. You can check functionality further by typing

```
cat /proc/net/atalk_iface
```

This command displays information on the devices to which atalkd has attached itself. For instance, on my system, this command reports the following:

```
eth0                 F500:DA  0000-FFFF  0
lo                   0000:00  0000-0000  0
```

This means that atalkd is servicing eth0 by using the address F500:DA (network address 62720, node address 218, expressed in hexadecimal), and is listening on networks 0 through FFFE (65534). The daemon has also attached itself to lo, the loopback interface.

A final test of basic atalkd functionality is to use the aecho command, which is AppleTalk’s equivalent of TCP/IP’s ping—it sends AppleTalk Echo requests to a specified host, waits for the reply, and prints some basic statistics. You can specify either the target computer’s AppleTalk name or its address (network and node, separated by a period, as in 41201.173). Here’s the result of giving the command aecho teela on my network:

```
14 bytes from 41201.173: aep_seq=0, time=0. ms
14 bytes from 41201.173: aep_seq=1, time=0. ms
14 bytes from 41201.173: aep_seq=2, time=0. ms
14 bytes from 41201.173: aep_seq=3, time=0. ms

---41201.173 AEP Statistics---
4 packets sent, 4 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/0
```

I terminated this test after four packets by pressing Ctrl+C.

> **NOTE**
> 
> You can use either a real Macintosh or another Netatalk-enabled computer as the target of the aecho command. You can’t use aecho on your own computer, though, at this stage of the configuration process.

At this point, I recommend terminating atalkd because in the next sections you’ll learn how to start it, afpd, and papd all with a single command.