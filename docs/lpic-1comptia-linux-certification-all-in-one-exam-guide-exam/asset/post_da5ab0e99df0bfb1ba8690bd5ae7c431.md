
The TCP protocol is used by upper-layer applications that require a high degree of data integrity, including

- Web servers
- E-mail servers
- FTP servers

However, the data fidelity offered by TCP comes at a cost, primarily in the form of latency. TCP requires a fair amount of network and processing overhead. Not all network applications actually require the high degree of data fidelity provided by TCP. Some upper-layer applications require less latency and can tolerate less reliability. These applications use the User Datagram Protocol (UDP) protocol instead of TCP. UDP functions in a manner similar to TCP; however, it is a *connectionless* protocol. With UDP, IP packets are sent unacknowledged. It is usually implemented with applications that send very small amounts of data at a time. It assumes that error checking and correction is either not necessary or will be performed by the application, avoiding the processing overhead.

In this respect, UDP is similar to sending someone a postcard through the mail. A postcard doesn't contain much data, and the receiver doesn't have to sign for it. Essentially, the sender assumes that the mail carrier is reasonably reliable and that the information on the postcard isn't important enough to require the receiver to sign for it. UDP works in much the same way. Some upper-layer applications that make use of UDP include

- Streaming audio and video
- VoIP

In addition to IP, TCP, and UDP, you also need to be familiar with the Internet Control Message Protocol (ICMP) protocol for your Linux*/LPIC-1 exam. ICMP is another core protocol in the IP protocol suite. It differs in purpose from TCP and UDP, which are transport protocols. The primary role of ICMP is to test and verify network communications between hosts.

For example, to test network connectivity, the ping utility will send ICMP Echo Request packets to a remote host. If the host receives them, it will respond with an ICMP Echo Response packet to the sender. If the ICMP Echo Response packet is received, the sender knows that a viable network connection exists between the sender and receiver and that the receiver is responding to network requests. If an ICMP Echo Response packet is not received, then the sender knows something is wrong and can begin troubleshooting communications.

For your Linux*/LPIC-1 exam, you also need to understand the concept of IP *ports*. Ports are provided by both the TCP and UDP protocols at the Transport layer. In essence, a port is a logical connection provided by TCP and UDP for upper-layer protocols. Ports allow a single host with a single IP address to provide multiple network services. Each service uses the same IP address but operates using a different TCP or UDP port number.

For example, suppose you have a network server with an IP address of 192.168.1.1 assigned to it. You could configure both a web server and an FTP server to run on it at the same time on this server. Each service will listen for requests on the interface assigned an IP address of 192.168.1.1. However, the web server runs on port 80, while the FTP server runs on ports 20 and 21. Requests sent to port 80 are handled by the web service, while information sent to ports 20 and 21 is handled by the FTP service.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_604_0.png)

> **NOTE** The FTP service is somewhat unique in that it uses two ports. One is for the control connection (port 21), while the other (port 20) is used for actually transferring data. Most services use only a single port.

You should become familiar with the various categories used to organize IP ports. Port numbers can range from 0 to 65536. The way these ports is regulated by the Internet Corporation for Assigned Names and Numbers (ICANN). There are three different categories that IP ports are lumped into:

- **Well-known ports**
  Reserved for specific services, well-known ports are those numbered from 0 to 1023, for example,
  - Ports 20 and 21: FTP
  - Port 23: Telnet
  - Port 25: SMTP
  - Port 80: HTTP
  - Port 110: POP3
  - Port 119: NNTP (news)
  - Ports 137, 138, 139: NetBIOS
  - Port 443: HTTPS
- **Registered ports**
  ICANN has reserved ports 1024 through 49151 for special implementations. Organizations can create their own network service and then apply for a registered port number to be assigned to it.
- **Dynamic ports**
  Dynamic ports are also called *private* ports. Ports 49152 through 65535 are designated as dynamic ports. They are available for use by any network service. They are frequently used by network services that need to establish a temporary connection. For example, the service may negotiate a dynamic port with the client. It will then use that port during the session. When the session is complete, the port is closed.

To make all of this work, you need to assign each host on the network an IP address. Let's discuss how this is done next.

### How IP Addresses Work

Every host on an IP-based network must have a unique IP address. An IP address is a Network layer (3) address that is logically assigned to a network host. Because the IP address is a logical address, it's not permanent. It can be changed at any time.

The IP address is different than the MAC address. The MAC address is a Data Link layer (2) hardware address that is burned into a ROM chip on every network board sold in the world. The MAC address is hard coded and can't be changed.

> **NOTE** The ARP protocol is used to map logical IP addresses assigned to systems to their hard-coded MAC addresses.

An IP address consists of four numbers, separated by periods. Examples of valid IP addresses include

- 12.34.181.78
- 192.168.1.1
- 246.270.3.8

> **NOTE** IPv4 addresses are sometimes called "dotted quad" addresses.

In decimal notation, each number must be between 0 and 255. For example, 192.168.1.1 is a valid IP address. Examples of *invalid* IP addresses include the following:

- 256.78.1.3 Can't use a value greater than 255
- 10.3.4 Must use four values

Each number in the address is actually an eight-bit binary number called an *octet*. Because each octet is a binary number, it can be represented as 0's and 1's. For example, the address 192.168.1.1 can be represented in binary form as

```
11000000.10101000.00000001.00000001
```

There are several simple ways to convert between the eight-bit binary address and the three-digit decimal version of an IP address. One option is to use the calculator software that comes with most Linux distributions (and even Windows) in Scientific mode. To convert a decimal IP address number to binary, enter the decimal version and then click the Bin option.

You can also go the other direction by entering a binary number in Bin mode and then switching to Dec mode, which will convert the binary number to its decimal equivalent.

If you're the mathematical type, you can also perform the conversion manually. Use the following to determine the value of each bit in a binary number:

- Bit 1 = 128
- Bit 2 = 64
- Bit 3 = 32
- Bit 4 = 16
- Bit 5 = 8
- Bit 6 = 4
- Bit 7 = 2
- Bit 8 = 1

For example, 11000000 = 128 + 64 = 192.

Some IP addresses are reserved and can't be assigned to a host. For example, the last octet in a host IP address can't be a 0. This is reserved for the address of the network segment itself that the host resides on. For example, the network address for the host assigned an IP address of 192.168.1.1 is 192.168.1.0.

In addition, the last octet of an IP address assigned to a host can't be 255. This is reserved for sending a broadcast to all hosts on the segment. In the preceding example, the broadcast address for a host with an IP address of 192.168.1.1 would be 192.168.1.255.

It's critical that you understand that every host on an IP-based network must have a unique IP address assigned to it. No two hosts on the same IP network can have the same IP address assigned. If the host resides on a public network, such as the Internet, it must use a globally unique IP address. You can apply to the Internet Assigned Numbers Authority (IANA) for a block of registered IP addresses. Once assigned, no one else in the world can use that IP address on a public network.

This actually introduces a key problem with IP version 4. The 32-bit addressing scheme used by IPv4 allows for a maximum of four billion possible unique addresses. This seemed like a lot of addresses back when IPv4 was originally defined. However, today this finite amount of available addresses is quickly running out.

To address this issue, a new version of IP has been proposed called IP version 6 (IPv6). IPv6 is expected to replace IPv4 over the next decade. Instead of 32 bits, IPv6 defines 128-bit IP addresses. This allows for a maximum of 3.4 × 10³⁸ total unique IP addresses! (Hopefully, this will be enough!)

IPv6 addresses are composed of eight four-character hexadecimal numbers, separated by colons instead of periods. For example, a valid IPv6 address could be 355B:FA77:4898:DAFC:200C:FBCC:A007:8973. Most Linux distributions support both IPv4 and IPv6.

The uptake of IPv6 has actually been slower than originally anticipated. Back in the early 1990s, IPv6 was known as IP Next Generation (IPNG) and was predicted to replace IPv4 in a very short time frame. Obviously, this didn't happen. One of the key reasons is the fact that a rather elegant interim solution has arrived at while everyone was working on IPv6: using private networks with Network Address Translation (NAT).

Using Network Address Translation, you can use a NAT router to present a single registered IP address to a public network while using private IP addresses on the network behind it. This is shown in Figure 15-3.

Using a NAT router has many advantages. Key among these is the fact that you can hide a huge private network behind one (or a couple) of public interfaces. This allows a large organization to implement their network and only need a relatively small number of globally unique public IP addresses.
