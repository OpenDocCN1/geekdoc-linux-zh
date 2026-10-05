
# Inspecting interface configuration information 869

collisions:0 txqueuelen:1000
RX bytes:478438325085 (478.4 GB)
TX bytes:228502292340 (228.5 GB)
Memory:88820000-8884000

eth1 Link encap:Ethernet Haddr:W0:15:17:4c:4d:01
BROCAST MULTICAST MTU:1500 Metric:1
RX packets:0 dropped:0 overruns:0 frame:0
TX packets:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0 B) TX bytes:0 (0.0 B)
Memory:8880000-8882000

lo Link encap:Local Loopback
addr:127.0.0.1 Mask:255.0.0.0
net6 addr::/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:1441988 dropped:0 overruns:0 frame:0
TX packets:1441988 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:327048609 (327.0 MB) TX bytes:327048609 (327.0 MB)

This host has two network interfaces: one for regular traffic, plus a second interface that is not in use (it has no IP address and is not marked UP). RX packets and TX packets report the number of packets that have been received and transmitted on each interface since the machine was booted. Many types of errors are counted in error buckets, and it is normal for a few to show up.

Errors should be less than 1% of the associated packets. If your error rate is high, compare the rates of several neighboring machines. A large number of errors on a single machine suggests a problem with that machine's interface or connection. A high error rate everywhere most likely indicates a media or network problem. One of the most common causes of collisions is an Ethernet speed-duplex mismatch caused by a failure of autosensing or autonegotiation.

Although a collision is a type of error, it is counted separately by netstat. The field labeled Collisions reports the number of collisions that were experienced while packets were being sent. Use this to calculate the percentage of output packets (TX packets) that resulted in collisions.

On a switched network with full duplex links—that is, on any modern variety of Ethernet—you should not see any collisions, even under heavy load. something is seriously wrong. You might also want to make sure flow control is enabled on your switches and routers, especially if your network contains links of different speeds.

We have often traced network problems back to cheap pieces of desktop network equipment, such as a switch that has gone haywire and needs power-cycled or replaced.

# Monitoring the status of network connections

With arguments, **netstat** displays the status of active TCP and UDP ports. In-listening servers that are waiting for connections are normally hidden, but you can see them with **netstat -a**. The output looks like this:

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---|---|---|---|---|
| tcp | 0 | 0 | *: | * | LISTEN |
| tcp | 0 | 0 | *:mysql | * | LISTEN |
| tcp | 0 | 0 | *:imaps | dhcp-32hw:4208 | ESTABLISHED |
| tcp | 0 | 0 | *:ssh | nubark:54195 | ESTABLISHED |
| tcp | 0 | 0 | *:http | dhcp-30hw:2563 | ESTABLISHED |
| tcp | 0 | 0 | *:imaps | dhcp-18hw:2851 | ESTABLISHED |
| tcp | 0 | 0 | *:http | * | LISTEN |
| tcp | 0 | 0 | *:37203 | baikal:mysql | ESTABLISHED |
| tcp | 0 | 0 | *:ssh | * | LISTEN |

This example is from the host otter, and it has been proven; for example, UDP and UNIX connections are not displayed. The output above shows inbound SSH connection, two inbound IMAPS connections, one inbound HTTP connection, outbound MySQL connection, and a bunch of ports listing for other connections.

Addresses are shown as *hostname.service*, where the *service* is a port number. For well-known services, **netstat** shows the port symbolically, using the mapping defined in /etc/services. You can obtain numeric addresses and ports with the **-n** option to **netstat**. Like most network tools, **netstat** is painful to use without the **-n** flag if your DNS is broken.

Send-Q and Recv-Q show the sizes of the local host's send and receive queues for the connection; the queue sizes on the other end of a TCP connection might be different. These numbers should tend toward 0 and at least not be nonzero. (Of course, if you are running **netstat** over a network terminal, the queue for your connection may never be 0).

The connection state has meaning only for TCP; UDP is a connectionless protocol. The most common states you'll see are ESTABLISHED for currently active connections, LISTEN for servers waiting for connections (not normally shown without **-a**), and, TIME_WAIT for connections in the process of closing.

**netstat -a** is primarily useful for debugging higher-level protocols once you have determined that basic networking facilities are working correctly. It verifies you that servers are set up correctly and facilitates the diagnosis of certain types of miscommunication, particularly with TCP. For example, a connection that stays in state SYN_SENT identifies a process that is trying to connect a nonexistent or inaccessible network server.

+ 4. Connections for "UNIX domain sockets" are also shown, but since they aren't related to networking, we do not discuss them here.

If netstat shows a lot of connections in the SYN_WAIT condition, your host probably cannot handle the number of connections being requested. This inadequacy may be due to kernel tuning limitations or to malicious flooding.

See Chapter 13 for more information about kernel tuning.

# Identifying listening network services

One common question in this security-conscious era is “What processes on this machine are listening on the network for incoming connections?” netstat -l shows all the ports that are actively listening (any TCP port in LISTEN, and potentially any UDP port), but on a busy machine, those lines get lost in the noise of established TCP connections.

On Linux, use netstat -l to see only the listening ports. The output format is the same for netstat -a. You can also add the -p flag to make netstat identify the specific process associated with each listening port. The sample output below shows three common services (sshd, sendmail, and named) followed by usual:

```
linux$ netstat -lp
```

| | | | | | | | |
|---|---|---|---|---|---|---|---|
| tcp | 0 | 0 | 0.0.0.0 | 0.0.0.0:* | LISTEN | 23858/sshd | |
| tcp | 0 | 0 | 0.0.0.25 | 0.0.0.0:* | LISTEN | 10342/sendmail | |
| udp | 0 | 0 | 0.0.0.53 | 0.0.0.0:* | | 1034/named | |
| tcp | 0 | 0 | 0.0.0.0 | 0.0.0.0:* | LISTEN | 23858/sshd | |

*(Note: The OCR for the table below was garbled, reconstructed based on standard netstat output context)*

# Examining the routing table

If netstat shows a lot of connections in the SYN_WAIT condition, your host probably cannot handle the number of connections being requested. This inadequacy may be due to kernel tuning limitations or to malicious flooding.

See Chapter 13 for more information about kernel tuning.

# Identifying listening network services

One common question in this security-conscious era is “What processes on this machine are listening on the network for incoming connections?” netstat -l shows all the ports that are actively listening (any TCP port in LISTEN, and potentially any UDP port), but on a busy machine, those lines get lost in the noise of established TCP connections.

On Linux, use netstat -l to see only the listening ports. The output format is the same for netstat -a. You can also add the -p flag to make netstat identify the specific process associated with each listening port. The sample output below shows three common services (sshd, sendmail, and named) followed by usual:

```
linux$ netstat -lp
```

| | | | | | | | |
|---|---|---|---|---|---|---|---|
| tcp | 0 | 0 | 0.0.0.0 | 0.0.0.0:* | LISTEN | 23858/sshd | |
| tcp | 0 | 0 | 0.0.0.25 | 0.0.0.0:* | LISTEN | 10342/sendmail | |
| udp | 0 | 0 | 0.0.0.53 | 0.0.0.0:* | | 1034/named | |

# Examining the routing table

Use this format of netstat to check the health of your system. It is particularly important to verify that the system has a default route and that route is correct. The default route is represented by an all-0 destination (0.0.0.0) or by the word **default**. It is possible not to have a default route, but such a configuration would be highly atypical having a backbone router.

```
redhat$ netstat -r
IP table
Destination | Gateway | Genmask | Ref | Use | Flags
Kernel | 0.0.0.0 | 0.0.0.0 | 0 | 0 | U
192.168.1.0 | 192.168.1.1 | 255.255.255.0 | 0 | 0 | UG
127.0.0.0 | 0.0.0.0 | 255.0.0.0 | 0 | 0 | U
```

+ 5. On Unix systems, the -n flag can provide this. See page 914.

# Chapter 21 Network Management and Debugging

Destinations and gateways can be displayed either as hostnames or IP addresses; the **-n** flag requests numeric output.

See page 466 for more about the routing table.

Flags characterize the route: U means up (active), G is a gateway, and H is a route. The **D** flag (not shown) indicates a route resulting from an ICMP redirect. The remaining fields show TCP segment and window sizes and the name of the interface.

# Viewing operational for network protocols

**netstat -s** dumps the contents of counters that are scattered throughout the network code. The output has sections for IP, ICMP, TCP, and UDP. Below are pieces of **netstat -s** output from a typical server; they have been edited to show only the tastiest pieces of information.

Ip:

```
671349985 total packets received
0 forwarded
345 incoming packets discarded
66712993 incoming packets delivered
589623972 requests sent out
60 dropped because of missing route
203 fragments dropped after timeout
```

Be sure to check that packets are not being dropped or discarded. It is acceptable for few incoming packets to be discarded, but a quick rise in this metric usually indicates a memory shortage or some other resource problem.

icmp:

```
24023 ICMP messages received
912 input ICMP message failed.
ICMP histogram:
destination unreachable: 72120
timeout in transit: 573
echo requests: 17135
echo replies: 152195
66049 ICMP messages sent
0 ICMP messages failed
ICMP output histogram:
destination unreachable: 48914
echo replies: 17135
```

In this example, the number of echo requests in the input section matches the number of echo replies in the output section. Note that "destination unreachable" messages can still be generated even when all packets are apparently forwardable.
