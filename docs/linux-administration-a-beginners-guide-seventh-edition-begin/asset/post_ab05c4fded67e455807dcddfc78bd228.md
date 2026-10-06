
infamous ping program. When a host receives the ICMP “Echo-Request” message, it responds with an ICMP “Echo-Reply” message. This allows the sender to confirm that the other host is up, and because we can see how long it takes the message to be sent and replied to, we can get an idea of the latency of the network between the two hosts.

## Headers

Earlier in the chapter, you learned that a TCP/IP packet over Ethernet is a series of headers for each protocol, followed by the actual data being sent. Packet headers, as they are typically called, are simply these pieces of information that tell the protocol how to handle the packet.

In this section we look at some of these headers (Ethernet, IP, TCP, UDP) using tcpdump tool. Most Linux distributions have it preinstalled, but if your distro doesn’t, you can quickly install it using the package management suite in your Linux distro.

> * TIP You must have superuser privileges to capture packets with tcpdump.

## Ethernet

Ethernet has an interesting history. As a result, there are two common types of Ethernet headers: 802.3 and Ethernet II. Frankly, although they both look similar, you can use a simple test to tell them apart. Let’s begin looking at the contents of the Ethernet header (see Figure 11-4).

The Ethernet header contains three entries: the destination address, the source address, and the packet’s protocol. Ethernet addresses—also called Media Access

| Full Ethernet Packet (46–1500 bytes) | | | | |
|---|---|---|---|---|
| Destination Address | Source Address | Type | Data | CRC |
| 6 | 6 | 2 | Up to 1486 bytes | 4 |
| | | 0800 | IP Datagram | |
| | | Type 0800 means “data” is an IP Datagram | | |

**Figure 11-4** The Ethernet header

are 48-bit (6-byte) numbers that uniquely identify every Ethernet card in the world. Although it is possible to change the MAC address of an interface, this is not recommended, as the default is guaranteed to be unique, and all MAC addresses on a LAN segment should be unique.

> NOTE A packet that is sent as a broadcast (meaning all network cards should accept this packet) has the destination address set to ff:ff:ff:ff:ff:ff.

The packet's protocol type is a 2-byte value that tells us what protocol packet should be delivered to the receiver's side. For IP packets, this value is 0800 (decimal 2048).

The packet we have just described is an Ethernet II packet. (Typically, it is just called Ethernet.) In 802.3 packets, the destination and source MAC addresses remain in place; however, the next 2 bytes represent the length of the packet.

The way you can tell the difference between the two types of Ethernet is that for Ethernet II, the protocol type value is greater than or equal to 1536, while the protocol type field value in 802.3 is less than 1500. In other words, any Ethernet header where the protocol type field value is less than 1500 is really an 802.3 packet. Realistically, you won't see many (if any) 802.3 packets.

## Viewing Ethernet Headers

To see the Ethernet headers on your network, run the following command:

```
[root@server]# tcpdump -e
```

This tells tcpdump to display the Ethernet headers along with the TCP and IP headers in its output.
Now generate some traffic by visiting a website, or use SSH to communicate with another host. Do so to generate output like:

```
15:46:08.026966 00:d7:6b:20:17 00:4b:bc:15:9f ethertype IPv4
(0x0800), length 191: ip 10.2.2.24769: Flags [P], seq
1724400-1724976, ack 529, win 5740, options [nop,nop,TS 593457613
ecr 1354193], length 576
```

The start of each line is a timestamp of when the packet was seen. The next two entries in the lines are the source and destination MAC addresses, respectively, for the first line. the source MAC address is 00:d7:6b:20:17 and the destination MAC address is the packet's type. In this case, tcpdump saw 0x800 and automatically converted it to ip for us so that it would be easier to read.

If you don't want tcpdump to convert numbers to names (especially handy when your DNS resolution is not working), you can run:

```
[root@server]# tcpdump -e -nn
```

The -n option tells tcpcdump to not make name resolution. The same preceding output without name resolution would look like this:

```
15:46:08.026966 0d:0:b7:6b:20:17 10:4b:bc:15:9f ethertype IPv4
(0x0800), length 191: 10.2.2.1.22 > 10.2.2.2479: Flags [P], seq
1724400:1724976, ack 529, 5740, options [nop,nop,ts 59345713
ecr 1354193], length 576
```

```
15:46:08.044151 10:4b:bc:15:9f 0d:0:b7:6b:20:17 ethertype IPv4
(0x0800), length 191: 10.2.2.1.22 > 10.2.2.2479: Flags [P], seq
172440:1724976, ack 529, 5740, options [nop,nop,ts 59345713
ecr 1354193], length 576
```

Note that in each of the new output, the host name became 10.2.2.1 and the port number became 22. We will discuss the meaning of the rest of the lines in the section "TCP", later.

## IP (IPv4)

The Internet Protocol has a slightly more complex header than Ethernet, as you can see in Figure 11-5. The first value in the IP header signifies the version number.

> NOTE The version of IP that is most common today is version 4 (IPv4); version 6 (IPv6) has also become more common and offers many improvements over version 4, such as an increase in address space, more efficient routing, and auto-configuration.

| 4-bit Version | 4-bit Header Length | 8-bit Type of Service (ToS) | 16-bit Total Length (in bytes) |
|---|---|---|---|
| 16-bit Identification | 3-bit Flags | 13-bit Fragment Offset | |
| 8-bit Time to Live (TTL) | 8-bit Protocol | 16-bit Checksum | 20 bytes |
| 32-bit Source IP Address | | | |
| 32-bit Destination IP Address | | | |
| Options (if any) | | | |
| Data (if any) | | | |

Figure 11-5 The IP header

The next value is the length of the IP header itself. You need to know the length of the header because optional parameters may be appended to the base header. The header length tells you how many, if any, options are there. To get the count of the total IP header, multiply this number by 4, indicating that there are 20 bytes in the complete header. The Type of Service (ToS) header indicates what kind of treatment should be given to the packet. As of this writing, the only defaults are minimized delay, maximized throughput, and minimized cost. See RFC 1340 (www.faqs.org/rfc/1340.html) and RFC 1349 (www.faqs.org/rfc1349.html) for more details. The use of ToS bits is sometimes referred to as "packet counting"; they are used by networking devices for the purpose of rate shaping and prioritization.

The total length tells you how much the complete packet is, including the IP and TCP headers, but not the Ethernet headers. This value is represented in bytes. An IP packet cannot be longer than 65,535 bytes.

The identification field is supposed to be a unique number used by a host to identify a packet. The flags in the IP packet indicate whether the packet is fragmented. Fragmentation occurs when an IP packet is larger than the maximum transmission size (MTU) between two hosts. For example, Ethernet's MTU is 1500 bytes. If we have a 4000-byte (3980 data + 20 byte header) IP packet that needs to be sent over Ethernet, the packet will be fragmented into three smaller packets. The first packet can be 1500 bytes (1480 data + 20 byte header), the second packet can also be 1500 bytes (1480 data + 20 byte header), and the last packet will be 1040 bytes (1020 data + 20 byte header).

The fragment offset tells you which part of the complete packet you are receiving. Continuing with the 4000-byte IP packet example, the first fragment will include 0-1479 of data and will have an offset of 0. The second fragment will include 1480-2959 of data and will have an offset of 185 (1480/8). The third and final fragment will include 2960-3999 of data and will have an offset of 370 (or 2960/8). The receiving stack will take these three packets and reassemble them into one large packet before passing it the stack.

> NOTE IP fragments don't happen frequently over the Internet. Thus, many firewalls take a paranoid approach about dealing with IP fragments, since they can be a source of denial-of-service (DoS) attacks.
