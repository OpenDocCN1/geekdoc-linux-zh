
## Getting Around IPTraf

IPTraf is menu driven; therefore, it proves itself almost immediately valuable to most network administrators. Figure 15.7, shows IPTraf's Main menu. The cursor keys can be used to navigate the window, or each menu also has a short cut key (highlighted) associated with it.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_307_0.png)

Figure 15.7 IPTraf Main menu.

A closer look at each of the functions supported by IPTraf follows.

## IP Traffic Monitor

The IP traffic monitor allows monitoring of IP traffic on a specific interface or on all interfaces recognized by the Linux kernel. Figure 15.8 shows an example of the IP traffic monitor.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_307_1.png)

Figure 15.8 IP traffic monitor screen.

The top portion of the IP traffic monitor reports TCP connections. Figure 15.8 shows a telnet connection (port 23) between 192.168.1.254 and 192.168.1.101. The IPTraf output also shows that station 192.168.1.254 has sent 372 packets over the TCP connection and 192.168.1.101 has sent 366.

The flags column reports how the flags were set in the last TCP packet as defined in RFC 793, "Transmission Control Darpa Internet Program Protocol Specification." Table 15.2 summarizes the TCP flags.

| Table 15.2 IP Traffic Monitor TCP Flags |
|---|---|---|
| IP Traffic Monitor Abbreviation | TCP Abbreviation | Meaning |
| A | ACK | Acknowledgment |
| P | PSH | Push all data to queue |
| U | URG | Packet is marked urgent |
| S | SYN | Synchronization during handshaking. |

IPTraf also will report resets with RST, unacknowledged FINs with DONE, and a properly closed connection with CLOSED. The packet and window size of each of the connections also can be viewed by pressing the m (more) key.

The bottom window in IP traffic monitor shows the most recent non-TCP traffic. In Figure 15.8, this was ICMP-echo requests (pings) and an address resolution protocol (ARP) request.

The bottom of the screen contains two lines. The first line is a real-time view of the packet count for IP, TCP, UDP, ICMP and non-IP traffic.

The second line is the menu for IP traffic monitor. The up and down arrows let you scroll through information when more than one screen is available. The w key switches between the top TCP window and the bottom, all other traffic window.

As mentioned, the m key will report the packet and window size of the TCP connections.

The s key allows the TCP connections to be sorted either using the packet or byte count, which will result in the same ordering; however, the command is useful because the IP traffic monitor does not sort in real time. With the sort command, the connections with the most traffic will "float" to the top of the list.

The x key is used to return to IPTraf's main window.

## General Interface Statistics

The General Interface Statistics screen gives a simple breakdown of traffic for all interfaces as shown in Figure 15.9. The counters include IP packets, non-IP (such as IPX), and bad IP, which are packets that can be identified by the IP header, but something in the header is not compliant with the IP protocol.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_309_0.png)

Figure 15.9 General Interface Statistics screen.

## Specific Interface Statistics

The Specific Interface Statistics allows the administrator to examine the IP statistics related to a particular configured interface. Figure 15.10 shows the statistics for eth0.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_309_1.png)

Figure 15.10 Specific Interface Statistics for eth0.

In addition to the breakdown of the types of IP packets, the lower portion of the screen also shows the throughput—both inbound and outbound. The specific interface statistics can be useful for quickly identifying possible problems when troubleshooting a network problem. Refer back to Figure 15.10, and you'll notice the number of ICMP packets is very high when compared to the total number of packets. A ping flood caused this.

## Statistical Breakdown

The Statistical Breakdown screen reports the number of packets received by two criteria, either the packet sizes on a particular interface or the TCP/UDP port of a particular interface. The statistical breakdown by packet size is shown in Figure 15.11 and by TCP/UDP port in Figure 15.12.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_310_0.png)

Figure 15.11 Statistical Breakdown—packet size.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_310_1.png)

Figure 15.12 Statistical Breakdown—TCP/UDP port.

## LAN Station Monitor

The LAN Station Monitor reports statistics based upon the Layer 2 address, or with Ethernet, the MAC address. Its use is limited, but it can be used in conjunction with other tools such as a sniffer to locate Layer 2 related problems. The LAN Station Monitor is shown in Figure 15.13.
