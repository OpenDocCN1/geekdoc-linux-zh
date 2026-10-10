
## Class B

Class B addresses are assigned to organizations that consist of a large number of networks and hosts. Therefore, many ISPs are assigned class B addresses.

| 0 | 1 | 1 | 6 | 31 |
|---|---|---|---|---|
| 1 | 0 | NETWORK |  | HOST |

- **First Octet**: Ranges from 128 to 191. The first two bits are 1 and 0.
- **Maximum Networks**: The network address is denoted by first and second octet. Therefore, $2^{14}$ = 16,384 class B networks are possible.
- **Maximum Hosts per Network**: Hosts are denoted by the last two octets. Therefore, $2^{16}$ - 2 = 65,534 hosts are possible per network.

## Class C

Class C addresses are used by organizations consisting of a small number of hosts per network.

| 0 | 1 | 2 | 24 | 31 |
|---|---|---|---|---|
| 1 | 1 | 0 | NETWORK | HOST |

- **First Octet**: Ranges from 192 to 233. The first three bits are 1, 1, and 0.
- **Maximum Networks**: The network address is denoted by the first, second, and third octets. Therefore, $2^{21}$ = 2,097,152 class C networks are possible.
- **Maximum Hosts per Network**: Hosts are denoted by the last octet. Therefore, $2^{8}$ - 2 = 254 hosts are possible per network.

## Class D

Class D is a reserved class that was designed to be used to send multicast messages to a group of hosts.

| 0 | 1 | 2 | 3 | 31 |
|---|---|---|---|---|
| 1 | 1 | 1 | MULTICAST ADDRESS |  |

- **First Octet**: Ranges from 224 to 239. The first four bits are 1, 1, 1, and 0.

## Class E

Class E is a reserved class. No IP addresses that fall under this class are assigned on the Internet.

| 0 | 1 | 2 | 3 | 4 | 31 |
|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | RESERVED |  |

- **First Octet**: Ranges from 240 to 255. The first five bits are 1, 1, 1, 1, and 0.

## Subnet Masks

Network addresses and host addresses are identified by the use of subnet masks. A *subnet mask* is a series of bits that match the network portion of a given address. For example, the following would be the network mask for a class B IP address:

```
11111111   11111111   00000000   00000000
```

The preceding mask would be 255.255.0.0 in dotted decimal notation.

## CIDR (Classless Inter-Domain Routing)

Because of the tremendous growth of the Internet, the five IP classes just listed were not sufficient to accommodate the many network schemes needed.

CIDR addresses, which were designed to meet this growing need, are denoted using the following notation:

```
`PREFIX`/mask
```

where *PREFIX* is the IP address prefix, and *mask* is the length of the network mask. For example:

```
`192.168.1.0/24`
```

Here, the PREFIX is 24 bits long, while the suffix is the remaining 8 bits. Therefore, this CIDR class will include the following IP addresses: 192.168.1.0–192.168.1.255.

## Loopback

The following range is referred to as a “loopback” range:

```
`127.0.0.0/8`
```

This range is used to designate the loopback address of the local host. Any packet sent to an address in this range will revert back to the host. Note that packets destined for an IP address in the loopback range do not propagate to the hardware network device, and therefore are never placed on the physical network wire.

## Private Addresses

The Internet Assigned Numbers Authority (IANA) has reserved the following three IP blocks for private intranets:

```
`10.0.0.0–10.255.255.255`  (CIDR Notation: `10.0.0.0/8`)
`172.16.0.0–172.31.255.255` (CIDR Notation: `172.16.0.0/16`)
`192.168.0.0–192.168.255.255` (CIDR Notation: `192.168.0.0/16`)
```

## Protocol Headers

RFC (Request For Comments) documents provide detailed information on the implementation of TCP/IP protocols. These documents contain protocol header information, a few examples of which are listed here.

## IP (Internet Protocol) Header

The following represents the layout of the IP header. The digits on the top of the header represent a byte each.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_35_0.png)

Usually, IP headers do not contain the Options field and are therefore 20 bytes long. When the Options field is present, its actual length is represented by the Total Length field which contains the length of the entire packet (header and data). Please see RFC 791 for more details: [http://www.faqs.org/rfcs/rfc791.html](http://www.faqs.org/rfcs/rfc791.html).

## TCP (Transmission Control Protocol) Header

Every TCP packet is encapsulated within the Data field of an IP packet, which immediately follows the IP header. The following represents the layout of a TCP header. Note that the digits on the top of the header represent a byte each.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_35_1.png)

Please see RFC 793 for more details: [http://www.faqs.org/rfcs/rfc793.html](http://www.faqs.org/rfcs/rfc793.html).

## UDP (User Datagram Protocol) Header

Similar to TCP, every UDP packet is also encapsulated within the Data field of an IP header. The following represents the layout of a UDP header. The digits on the top of the header represent a byte each.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_36_0.png)

Please see RFC 768 for more details: http://www.faqs.org/rfcs/rfc768.html.

## ONLINE RESOURCES

In addition to the various online resources mentioned throughout the book, this section contains pointers to additional resources that can be used to stay up to date with the latest happenings in the security arena.

> Remember to check <http://www.hacknotes.com/> for the latest security resources.

## Hacking Tools

The following table lists the most popular hacking tools used by hackers today. Most of the tools mentioned in this table are used throughout Part I of this book. URLs from which these tools can be downloaded are also provided.

| Name | Description | Location |
|:---|:---|:---|
| Aircrack | Popular WEP cracker (802.11b) | <http://airsnort.shmoo.com/> |
| Adore | Backdoor | <http://www.team-teso.net/releases.php> |
| Amap | Identifies remote applications | <http://www.tcr.org/releases.php> |
| Cheops | GUI based tool that identifies information about hosts on a network | <http://www.marko.net/cheops/> |
| Desproxy | Command-line tool that tunnels TCP traffic through web proxies | <http://desproxy.sourceforge.net/> |
| Dsniff | A suite of network sniffing tools | <http://monkey.org/~dugsong/dsniff/> |
| Ethereal | GUI based network sniffer | <http://www.ethereal.com/> |
| Etercap | Ncurses based network sniffer | <http://etercap.sourceforge.net/> |
| Fake-IP | Performs Denial of Service attacks on 802.11 networks | <http://www.loud-fat-bloke.co.uk/w80211.html> |
| Firewall | A tool similar to traceroute that determines gateway access control lists | <http://www.packetfactory.net/projects/firewall/> |
| Fragroute | Intercepts, modifies, and rewrites network traffic | <http://www.monkey.org/~dugsong/fragroute/> |
| Hping2 | Command-line TCP/IP packet assembler and analyzer | <http://www.hping.org/> |

| Name | Description | Location |
|:-------|:--------------|:-----------------|
| Hunt | Performs TCP hijacking | http://lin.fsld.cvut.cz/-kra/index.html#HUNT |
| Hydra | Active password brute forcer | http://www.thc.org/releasess.php |
| John | Passive password cracker | http://www.openwall.com/john/ |
| Kismet | Network sniffer that identifies wireless networks in the area | http://www.kismetwireless.net/download.shtml |
| Knark | Rootkit | http://www.packetstormsecurity.org/ |
| Linux Root Kit (LRK) | Rootkit | http://www.packetstormsecurity.org/ |
| Loki2 | Backdoor | http://www.phrack.com/show.php?p=51&a=6 |
| Nemesi s | Command-line network packet injection suite | http://www.packetfactory.net/projects/nemesi s/ |
| Nessus | Vulnerability scanner | http://www.nessus.org/ |
| Netcat | Reads and writes data across networks. TCP and UDP protocols are supported. | http://www.atstake.com/research/tools/network_utilities/ |
| Ngrep | Similar to the grep command, but used to analyze network packets. | http://www.packetfactory.net/projects/ngrep/ |
| Nikto | Web server and web application vulnerability scanner | http://www.cirt.net/code/nikto.shtml |
| Nmap | Port scanner | http://www.insecure.org/nmap/ |
| Openssl | Establishes SSL connections | http://www.openssl.org/ |
| Snmpwalk | SNMP query tool | http://www.net-snmp.org/ |
| Snort | Network sniffer and intrusion detection system | http://www.snort.org/ |
| Spike Proxy | HTTP and HTTPS proxy | http://www.immunitysec.com/spikeproxy.html |
| Stunnel | SSL wrapper | http://www.stunnel.org/ |
| Tcpdump | Command-line sniffer | http://www.tcpdump.org/ |
| Tormkit | Rootkit | http://www.packetstormsecurity.org/ |
