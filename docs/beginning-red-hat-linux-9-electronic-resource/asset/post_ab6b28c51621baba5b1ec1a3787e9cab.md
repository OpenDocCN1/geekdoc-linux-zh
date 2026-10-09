
## tcpdump -i eth0 -l -q -X src or dst port 23

```text
tcpdump: listening on eth0
12:11:51.070377 fred.3335 > bob.telnet: tcp 0 (DF)
0x0000    4500 0030 317b 4000 8006 3342 0a04 4101    E..0{@.3.B.A.
0x0010    0a04 4102 0d07 0017 24e6 7419 0000 0000    ..A..$.t.....
0x0020    7002 2000 26f7 0000 0204 05b4 0101 0402    p...&.......
```

If we look carefully at the packet log, we can find the Password prompt and see what the user typed in response. The password has been highlighted to make it easier to see, but hackers don't need that much help – they'll probably use an automated password sniffer that'll decode the packets for them:

```text
12:12:02.265222 bob.telnet > fred.3335: tcp 10 (DF) [tos 0x10]
0x0000    4510 0032 9d51 4000 4006 075a 0a04 4102    E..2Q@.Z.A.
0x0010    0a04 4101 0017 0d07 f2e7 55fc 24e6 746e    ...$...tn.
0x0020    5018 16d0 2c48 0000 5061 7773 7764 7264    P...Password
0x0030    3a20
:
12:12:02.455557 fred.3335 > bob.telnet: tcp 0 (DF)
0x0000    4500 0028 4a7b 4000 8006 1a4a 0a04 4101    E..J@...J.A.
0x0010    0a04 4102 0d07 0017 24e6 746e 2f67 5606    ..A....$....
```

```text
12:12:03.699442 fred.3335 > bob.telnet: tcp 1 (DF)

0x0000 4500 0029 4e7b 4000 8006 1649 0a04 4101 E..N{@...I..A.
0x0010 0a04 4102 0d07 0017 24e6 7471 f267 5606 ..A...$..S.tq.gV.
0x0020 5018 21a8 a534 0000 6420 2020 P.!.4..d....
```

This is what we mean when we say that the telnet protocol sends passwords in plain text across the network. If that network uses broadcast media, then every machine on the same network segment as the sender receives the unencrypted password on its network interface. Most of the time, the other machines will just ignore this data, but all it takes is one of them to be running a promiscuous mode packet logger like tcpdump and all the passwords sent by telnet can be captured. Ftp suffers from a similar vulnerability. Fortunately, there are secure alternatives to both telnet and ftp (ssh and sftp respectively) that encrypt all data they send over the network using strong encryption techniques so the eavesdropper is not able to glean any useful information from the packets.

Another packet analyzer that can be installed from the Red Hat Linux 9 CDs is called Ethereal. This has a graphical front end that makes it much easier to set up filters and interpret the contents of packets. When Ethereal is started (as root, by simply typing ethereal at the command prompt – once the Ethereal RPM has been installed, of course!), the main window opens. The Capture | Start menu option opens another window where capture options can be set:

![](img/b852150740856958b10aff9e8c9d2adc_543_0.png)

Note the check box to put the interface (eth0) in promiscuous mode, so packets not intended for this machine can be captured. Once capturing is running, another window is updated continuously with packet counts.

![](img/b852150740856958b10aff9e8c9d2adc_544_0.png)

With the options chosen in the example capture window, the main display is also updated in real time:

![](img/b852150740856958b10aff9e8c9d2adc_544_1.png)

This example shows the start of an `ssh` session between two machines. This time, we won't be seeing any plain text passwords!

The point of showing `tcpdump` and `ethereal` is not to encourage you to go sniffing for packets on networks, but rather to illustrate just how easy it is to capture sensitive information such as passwords that are sent across broadcast networks, such as Ethernet. However, if you make sure that you use protocols such as `ssh` and `sftp` that encrypt sensitive data, then it won't matter if someone is capturing the packets you send.

## Firewalls

Firewalls are another useful tool for improving the security of our system. They come in different flavors, but all do essentially the same thing; network traffic passing through the firewall is analyzed and the decision about what to do with the traffic (let it through, throw it away and tell the sender, throw it away and don't tell the sender, etc.) is made based on the rules configured by the firewall administrator.

Some firewalls analyze network traffic at the packet level; these are called "packet filters". They can work with any network traffic, but can implement only fairly simple rules based on the contents of the packet header (typically where the packet came from, where it's going to and what flags are set). Other firewalls understand more about the higher level protocols used for e-mail and web browsing. They can perform more complex tasks such as scanning e-mail attachments for viruses, or requiring users to authenticate themselves before allowing access to certain Web sites. In a typical corporate environment, the protection provided by simple packet filtering firewalls is enhanced with more sophisticated firewalls and proxies that can analyze the contents of the packets as well as their headers.

Since the Linux kernel has built-in packet filtering capabilities, we'll look at how we can configure these to enhance the security of our Red Hat Linux system.

## Network Connections

Before we get into the mechanics of configuring the Red Hat Linux built-in firewall, we need to understand how network connections work. For TCP/IP connections, there are two basic protocols; TCP (Transmission Control Protocol) and UDP (Universal Datagram Protocol).

TCP is a connection-oriented protocol. This means that when two machines wish to communicate via TCP, their TCP stacks negotiate a connection and the application (such as a Web browser talking to Web server using HTTP), and TCP ensures that packets are delivered to the application in the right order, with no duplicates. The mechanism for setting up a connection involves the exchange of TCP packets between the systems that have different flags set in their headers. First, the client (that's the machine that wants to establish a connection) sends the server (the machine the client wants to connect to) a TCP packet with the SYN flag set. The server replies with a packet whose header has both the SYN and ACK flags set, and when the client receives this packet, it sends one back with just the ACK bit set. From this point on, the connection is established, and the client and server can exchange packets.

When the connection is no longer required, either party can request that it is closed by sending the other end a TCP packet with the FIN flag set. The recipient replies with a packet having the ACK flag set, then performs whatever termination steps are required by the application. When this is done, a packet with the FIN flag set is sent back to the end that initially requested the connection to be closed. When this is acknowledged with a packet where the ACK bit is set, the connection is finished.

UDP is a much simpler, connection-less protocol. All that happens here is that the originator sends the UDP datagram to the recipient, and the network layer tries its best to deliver it. Unlike TCP, delivery is not guaranteed, and datagrams traveling over long distances may go by different routes and therefore arrive out of order at the other end. All the logic for synchronizing client and server, or re-trying failed packets, has to be handled by the application code.

It is important that we understand the differences between TCP and UDP when configuring firewalls. With TCP, the direction of the connection (i.e. incoming, where the client is remote and the server is on our machine, or outgoing where the client is local and the server is remote) is determined by the exchange of SYN, SYN+ACK, ACK packets at the start of the connection, but with UDP, there is no connection, so incoming and outgoing simply refer to the direction of the packet.

## Configuring the Red Hat Linux Firewall

Configuring the Red Hat Linux firewall is very straightforward. Start the Security Level Configuration application by choosing **Main Menu | System Settings | Security Level**, or by typing `redhat-config-securitylevel` at the command prompt. If you are not logged on as root, and you haven't recently supplied the root password to enable you to update system wide settings, you'll be prompted to do that before the Security Level Configuration starts. When it does, you'll see this window.

![](img/b852150740856958b10aff9e8c9d2adc_546_0.png)
