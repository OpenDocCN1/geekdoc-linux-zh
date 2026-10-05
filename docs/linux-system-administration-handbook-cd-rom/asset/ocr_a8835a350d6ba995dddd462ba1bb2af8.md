# 23.4 PPP

your application. I normally like to have the S11 register set at its lowest setting. This can be done by adding the line, just before the telephone number in the chatfile.

OK
ATS11=55

After PPP is configured, start the daemon with ppp-on, and perform the following test:

The output from netstat -nr, should read:

| Kernel routing table |
| Destination Gateway | Genmask | Flags Metric Ref Use Iface |
| 555.666.777.888.0.0.0 | 255.255.255.255 | UH | 0 | 0 | 0 | ppp0 |
| 192.168.1.0 0.0.0 | 255.255.255.0 | U | 0 | 0 | 28 | eth0 |
| 127.0.0.0 0.0.0 | 255.0.0.0 | U | 0 | 14 |
| 0.0.0.0 555.666.777.888 | 0.0.0.0 | UG | 0 | 0 | ppp0 |

The output from ifconfig, should read:

```
lo Link enc:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST RUNNING MTU:2000 Metric:1
RX packets:0 errors dropped:0 overflows:0
TX packets:42 errors dropped:0 overflows:0
p0 Link enc:Point-Point Protocol
inet addr:111.222.333.444 P-t-P:555.666.777.888
Mask:255.255.255.0
UP POINTTOPOINT RUNNING MTU:552 Metric:1
RX packets:0 errors dropped:0 overflows:0
TX packets:0 errors dropped:0 overflows:0
0 Link enc:10Mbps Ethernet Haddr:02:06:8C:49:05:57
inet addr:192.168.1.1 Bcast:192.168.1.255Mask:255.255.255.0
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:0 errors dropped:0 overflows:0
TX packets:26 errors dropped:0 overflows:0
Interrupt:5 Base address:0x300
```

Try to ping:
localhost: ping 127.0.0.1
your ISP: ping isname.net
Other IPs on the network

Another good test would now be to use a Web browser and try to pull up your favorite Web page, provided by your ISP.
After testing the link, execute ppp-off. After this, attempting to telnet to a remote host should come back with an error stating "host not found."