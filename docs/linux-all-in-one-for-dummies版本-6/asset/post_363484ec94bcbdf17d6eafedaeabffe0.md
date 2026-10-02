
## Checking Out TCP/IP Networks

After you configure Ethernet and TCP/IP (whether during Linux installation or by running a network configuration tool or command later), you can use various networking applications without much problem. On the off chance that you do run into trouble, Linux includes several tools to help you monitor and diagnose problems.

### Checking the network interfaces

The /sbin/ifconfig command, which may need to be installed in some distributions, is used to view the currently configured network interfaces. The ifconfig command is used to configure a network interface (that is, to associate an IP address with a network device). If you run ifconfig without any command-line arguments, the command displays information about current network interfaces.

This output displayed will show the loopback interface (lo) and any installed network cards as well as if they are currently active on this system. For each interface, you can see the IP address, as well as statistics on packets delivered and sent. If the Linux system has a dial-up PPP link up and running, you also see an item for the ppp0 interface in the output.

### Checking the IP routing table

The other network configuration command, /sbin/route, also provides status information when you run it without a command-line argument. If you're having trouble checking a connection to another host (that you specify with an IP address), check the IP routing table to see whether a default gateway is specified. Then check the gateway's routing table to ensure that paths to an outside network appear in that routing table.

Typical output from the /sbin/route command looks like the following:

```
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.0.0 * 255.255.255.0 U 0 0 0 eth0
192.168.0.0 * 255.255.255.0 U 0 0 0 eth1
169.254.0.0 * 255.255.0.0 U 0 0 0 eth1
default 192.168.0.1 0.0.0.0 UG 0 0 0 eth0
```

As this routing table shows, the local network uses the eth0 and eth1 Ethernet interfaces, and the default gateway is the eth0 Ethernet interface. The default gateway is a routing device that handles packets addressed to any network other than the one in which the Linux system resides. In this example, packets addressed to any network address other than those beginning with 192.168.0 are sent to the gateway — 192.168.0.1. The gateway forwards those packets to other networks (assuming, of course, that the gateway is connected to another network, preferably the Internet).

### Checking connectivity to a host

To check for a network connection to a specific host, use the ping command. ping is a widely used TCP/IP tool that uses a series of Internet Control Message Protocol (ICMP, pronounced EYE-comp) messages. ICMP provides for an echo message to which every host responds. Using the ICMP messages and replies, ping can determine whether the other system is alive and can compute the round-trip delay in communicating with that system.

The following example shows how I run ping to see whether a system on my network is alive:

```
ping 192.168.0.1
```

Here’s what this command displays on my home network:

```
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=63 time=0.256 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=63 time=0.272 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=5 ttl=63 time=0.275 ms
--- 192.168.0.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 3999ms
rtt min/avg/max/mdev = 0.256/0.267/0.275/0.016 ms
```

In Linux, ping continues to run — unless you used the -c option — until you press Ctrl+C to stop it; then it displays summary statistics showing the typical time it takes to send a packet between the two systems. On some systems, ping simply reports that a remote host is alive. You can still get the timing information by using appropriate command-line arguments, however.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_213_0.png)

The ping command relies on ICMP messages that many firewalls are configured to block. Therefore, ping may not always work and is no longer a reliable way to test network connectivity. If ping fails for a specific host, don’t assume that the host is down or not connected to the network. Typically, you can use ping to check connectivity within your local-area network (LAN).

### Checking network status

To check the status of the network, use the netstat command. This command displays the status of network connections of various types (such as TCP and UDP connections). You can view the status of the interfaces quickly by typing netstat -i, which results in output similar to the following:

```
Kernel Interface table
Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0 1500 0 613175 0 0 1 574695 0 0 0 BMRU
eth1 1500 0 4298 0 0 0 1375 1 0 0 BMRU
lo 16436 0 3255 0 0 0 3255 0 0 0 LRU
```

In this case, the output shows the current status of the loopback and Ethernet interfaces.

Table 4-2 describes the meanings of the columns.

### Meanings of Columns in the Kernel Interface Table

| Column | Meaning |
|---|---|
| Iface | Name of the interface |
| MTU | Maximum Transmission Unit — the maximum number of bytes that a packet can contain |
| Met | Metric value for the interface — a number indicating distance (in terms of number of hops) that routing software uses when deciding which interface to send packets through |
| RX-OK, TX-OK | Number of error-free packets received (RX) or transmitted (TX) |
| RX-ERR, TX-ERR | Number of packets with errors |
| RX-DRP, TX-DRP | Number of dropped packets |
| RX-OVR, TX-OVR | Number of packets lost due to overflow |
| Flg | A = receive multicast; B = broadcast allowed; D = debugging turned on; L = loopback interface (notice the flag on lo), M = all packets received, N = trailers avoided; O = no Address Resolution Protocol (ARP) on this interface; P = point-to-point interface; R = interface is running; and U = interface is up |

Another useful form of netstat option is -t, which shows all active TCP connections. Following is a typical result of typing netstat -t on one Linux PC:

```
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 localhost:2654 localhost:1024 ESTABLISHED
tcp 0 0 localhost:1024 localhost:2654 ESTABLISHED
tcp 0 0 LNB NECXAN.mrockv01.:ssh 192.168.0.6:1577 ESTABLISHED
```

In this case, the output columns show the protocol (Proto), the number of bytes in the receive and transmit queues (Recv-Q, Send-Q), the local TCP port in hostname:service format (Local Address), the remote port (Foreign Address), and the state of the connection.

Type `netstat -ta` to see all TCP connections — both active and the ones your Linux system is listening to (with no connection established yet). Here’s typical output from the `netstat -ta` command:

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 *:32769 *:* LISTEN
tcp 0 0 *:mysql *:* LISTEN
tcp 0 0 *:sunrpc *:* LISTEN
tcp 0 0 *:ftp *:* LISTEN
tcp 0 0 localhost.localdomain:ipp *:* LISTEN
tcp 0 0 *:telnet *:* LISTEN
tcp 0 0 localhost.localdomain:5335 *:* LISTEN
tcp 0 0 localhost.localdomain:smtp *:* LISTEN
tcp 0 0 192.168.0.9:45876 www.redhat.com:http ESTABLISHED
tcp 0 0 192.168.0.9:45877 www.redhat.com:http ESTABLISHED
tcp 0 0 192.168.0.9:45875 www.redhat.com:http ESTABLISHED
tcp 0 0 *:ssh *:* LISTEN
tcp 0 0 :::ffff:192.168.0.7:ssh :::ffff:192.168.0.3:4932 ESTABLISHED
```

### Sniffing network packets

Sniffing network packets sounds like something illegal, doesn’t it? It’s nothing like that. Sniffing simply refers to viewing the TCP/IP network data packets. The concept is to capture all the network packets so that you can examine them later.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_215_0.png)

If you feel like sniffing TCP/IP packets, you can use `tcpdump`, a command-line utility that comes with Linux. As its name implies, it dumps (prints) the headers of TCP/IP network packets.

To use `tcpdump`, log in as `root` and type the `tcpdump` command in a terminal window. Typically, you want to save the output in a file and examine that file later. Otherwise, `tcpdump` starts spewing results that flash by in the window. To capture
