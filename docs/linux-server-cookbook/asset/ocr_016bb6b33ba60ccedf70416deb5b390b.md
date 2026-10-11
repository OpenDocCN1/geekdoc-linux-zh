| [ src / dst ] net | Filter the network, optionally indicating if it is an src or a dst. |
| [ src / dst ] port | Filter the port, optionally indicating if it is an src or a dst. |
| [src / dst ] portrange | Filter a range port, optionally indicating if it is an src or a dst. |
| tcp / udp / icmp | Filter for one of the protocols indicated |
| arp | Filter for the arp protocol |

*Table 8.5:* Common options for the command firewall-cmd

Full filters are available for running the command man pcap-filter. It is possible to use special words “and” and “or” to combine several expressions. *Figure 8.32* shows an example filtering from the IP 10.0.0.28 and port 80:

```
root@ubuntu:~# tcpdump -i bridge0 -n “src host 10.0.0.218 and port 80” -c 1
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on bridge0, link-type EN10MB (Ethernet), snapshot length 26144 bytes
20:21:24.923973 IP 10.0.0.218.53772 > 10.0.0.220.80: Flags [S], seq 2901927797, wi n 64240, options [mss 1460,sackOK,TS val 2755969774 ecr 0,nop,wscale 7], length 0
1 packet received by filter
0 packets dropped by kernel
```

*Figure 8.32:* Output example for the command tcpdump

*Wireshark* is another popular solution for packet analyzing. The solution includes a CLI tool called tshark, which works similar to tcpdump, and a Graphical User Interface (GUI) to help inspect the information in the packet. *Figure 8.33* shows the output example for the command tshark filtering to the port 80 and the ip 10.0.0.218:

```
root@ubuntu:~# tshark -i bridge0 -f “tcp port 80 and src host 10.0.0.218” -c1
Running as user “root” and group “root”. This could be dangerous.
Capturing on ’bridge0’
** (tshark:4334) 20:37:13.112691 [Main MESSAGE] -- Capture started.
** (tshark:4334) 20:37:13.112998 [Main MESSAGE] -- File: “/tmp/wireshark_bridge04 CRNR1 pcapng”
1 0.000000000 10.0.0.218 → 10.0.0.220 TCP 74 58456 → 80 [SYN] Seq=0 Win=64 240 Len=0 MSS=1460 SACK\_PERM=1 TSval=2756921357 TSecr=0 WS=128
1 packet captured
```

*Figure 8.33:* Output example for the command tshark.

*Figure 8.34* shows the aspect of the *Wireshark* interface: