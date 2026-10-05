# TCP/IP and Network Management
CHAPTER 7

passwords in the clear, a cracker might a sniffer to sniff out their passwords. Because of this, tcpdump should not be installed setuid-root.

To detect whether a network interface is in promiscuous mode (and thus might have a sniffer running on it), use the ifconfig command to display the interface's configuration. The PROMIS flag will appear if the interface is in promiscuous mode:

```
# /sbin/ifconfig eth0
eth0 Link encap:Ethernet HWaddr 00:60:97:3E:F0:61
       inet addr:10.0.1.50 broadcast:10.0.1.255 Mask:255.255.255
       UP BROADCAST PROMISC MULTICAST MTU:1500 Metric:1
       RX packets:5 errors:0 dropped:0 overflows:0 frame:0
       TX packets:5 errors:0 dropped:0 overflows:0 carrier:5
       Collisions:0
       Interrupt:3 Base address:0x310
```

If you run tcpdump without any arguments, you get a listing of all the packets that pass through the network:

```
# /usr/sbin/tcpdump
tcpdump: listening on eth0
22:46:12.730048 renato.1445923871 > vishnu.nfs:100 readlink [nfs]
22:46:12.734224 tombolia.1012 > vishnu.808: udp 92
22:46:12.746873 tombolia.22 > atman.1023: P 142299991:1422300035(44)
→ 3799214399 win 32128 (DF) [tos 0x10]
22:46:12.763884 atman.1023 > tombolia.22: ack 44
→ win 32128 (DF) [tos 0x10]
22:46:12.778108 vishnu.808 > tombolia.1015: udp 56
22:46:12.780084 gerardo.144387013 > vishnu.nfs: [nfs]
22:46:12.781553 tombolia.22 > atman.1023: P 44:596(552)
→ ack 1 win 32128 (DF)
→ [tos 0x10]
```

The dump stops when you press Ctrl+C.

As you can see, tcpdump by default converts IP addresses to hostnames and port numbers to service names. It also attempts to interpret some packets (such as where the line ends with lookup [nfs]), which are NFS lookups. In some cases, the number of bytes that tcpdump dumps (68) may not be enough to decode the packet. In this case, you may use the -s option to increase the number (the -s option in Table 7.6).