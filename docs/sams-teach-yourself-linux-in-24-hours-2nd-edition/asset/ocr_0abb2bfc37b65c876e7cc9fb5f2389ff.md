```
eth0  Link encap:Ethernet  HWaddr 00:E0:98:04:AA:D5
inet addr:192.1.2.34  Bcast:192.1.2.0  Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:5 errors:0 dropped:0 overruns:0 frame:0
TX packets:5 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:100
Interrupt:3 Base address:0x300
```

![](bbox=[0.1, 0.32, 0.2, 0.42])

> If you do not see an active local loopback (lo) interface, use the ifconfig command with the lo and up options like this:
> # ifconfig lo up

As you can see, you now have an active Ethernet interface (eth0) and address (in this case, 192.1.2.34). If you're connected to a local network, use the ping command to try to test your connection. Type ping on the command line of a terminal window, followed by the IP address of another computer, like this:

```
# ping 192.1.2.36
PING 192.1.2.36 (192.1.2.36): 56 data bytes
64 bytes from 192.1.2.36: icmp_seq=0 ttl=64 time=0.6 ms
64 bytes from 192.1.2.36: icmp_seq=1 ttl=64 time=0.5 ms
64 bytes from 192.1.2.36: icmp_seq=2 ttl=64 time=0.5 ms
64 bytes from 192.1.2.36: icmp_seq=3 ttl=64 time=0.5 ms
64 bytes from 192.1.2.36: icmp_seq=4 ttl=64 time=0.5 ms

--- 192.1.2.36 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.5/0.5/0.6 ms
```

Press Ctrl+C to stop the ping command, which sends and records the time it takes (in thousandths of a second) for a "packet" of 64 characters to be sent and echoed back from a remote computer. The remote computer can be on a local network or halfway across the world.