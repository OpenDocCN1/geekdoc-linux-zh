![](bbox=[0.15, 0.07, 0.64, 0.36])

**Figure 11.8** _The 11nxconf client is a comprehensive administration tool for Linux that includes configuration controls for networking devices._

Note that you can also tell `11nxconf` that the adapter is a PCMCIA device. In addition, you can specify an optional I/O port or IRQ in special instances (as always, consult the PCMCIA-HOWTO when troubleshooting PC card problems). When you're finished, click on the Accept button. You can then click on the Act/Changes (activate changes) button and quit the program.

After you configure the interface, try using the `ping` command to test the speed and reliability of transmission and receipt of data packets across your LAN. For example, use `ping`'s -c (count) option, along with a number such as 3, followed by the name or IP address of a remote host on your LAN (or, if connected to the Internet, to a remote computer):

```
# ping -c 3 ascentia.home.org
PING asenitia.home.org (192.168.2.32): 56 data bytes
64 bytes from 192.168.2.32: icmp_seq=0 ttl=255 time=0.5 ms
64 bytes from 192.168.2.32: icmp_seq=l ttl=255 time=0.4 ms
64 bytes from 192.168.2.32: icmp_seq=2 ttl=255 time=0.4 ms

--- asenitia.home.org ping statistics --
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.4/0.4/0.5 ms
# ping -c 3 megan.staffnet.com
```