# Listing the Firewall Rules

iptables -v -L INPUT

The -v option produces more verbose output, including the interface name. Reporting the interface name is especially helpful when the machine has more than one network interface.

Using the same seven sample rules from the INPUT chain, the following shows what the listing output looks like using the -v verbose option:

```
```
> iptables -v -L INPUT

1  INPUT (policy DROP 0 packets, 0 bytes)
2  pkts bytes target  prot opt in out  source  target
3  32  3416 ACCEPT  all -- lo any  anywhere \
   anywhere
4  0 0 LOG  icmp -f any any anywhere \
   anywhere
   LOG level warning prefix "Fragmented ICMP: "
5  0 0 DROP   tcp -- any any anywhere \
   tcp flags:FIN,SYN,RST,PSH,ACK,URG/NONE
6  94 6586 ACCEPT  all -- any any anywhere \
   state RELATED,ESTABLISHED
7  1 65 ACCEPT  udp -- eth0 any 192.168.1.0/25 \
   my.host.domain  udp spts:1024:65535 dpts:domain state NEW
8  0 0 REJECT  tcp -- eth1 any anywhere \
   my.host.domain2  tcp dpt:auth reject-with icmp-port-unreachable
9  1 48 ACCEPT  tcp -- eth0 any 192.168.1.0/25 \
   my.host.domain  multicast dports http,https tcp spts:1024:65535 \
   flags:SYN,RST,ACK/SYN state NEW
```
```

Line 1 identifies the listing as being for the INPUT chain. The INPUT chain's default policy is DROP. 0 packets have been dropped by the default policy, accounting for 0 bytes of network traffic.

Line 2 contains the following column headings:

+   - **pkts** is the number of packets that have matched the rule.
+   - **bytes** is the number of bytes contained in the packets matching the rule.
+   - **target** refers to the target disposition of a packet matching the rule **ACCEPT**, **DROP**, **LOG**, or **REJECT**.
+   - **prot** is an abbreviation for *protocol*, which can be **all**, **tcp**, **udp**, or **icmp**, as well as a value from */etc/protocols*.
+   - **opt** stands for *fragmentation options*, which would have been set with either the *-f* or the *! -f* option. An **t** in the first space indicates the **t -f** option, which means to match either unfragmented packets or the first fragment in a series. An **f** in the second space indicates the *-f* option, which means to match the second and subsequent fragments.