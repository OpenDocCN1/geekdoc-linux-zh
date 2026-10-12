trouble checking a connection to another host (that you specify with an IP address), check the IP routing table to see whether a default gateway is specified. Then check the gateway’s routing table to ensure that paths to an outside network appear in that routing table.

A typical output from the /sbin/route command looks like this:

```
/sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.1.200   *               255.255.255.255 UH    0      0        0 eth0
192.168.1.0     *               255.255.255.0   U     0      0        0 eth0
127.0.0.0       *               255.0.0.0       U     0      0        0 lo
default         192.168.1.1     0.0.0.0         UG    0      0        0 eth0
```

As this routing table shows, the local network uses the eth0 Ethernet interface and the default gateway is also that Ethernet interface. The default gateway is a routing device that handles packets addressed to any network other than the one in which the Linux system resides. In this example, packets addressed to any network address other than ones that begin with 192.168.1 are sent to the gateway — 192.168.1.1 — and the gateway forwards those packets to other networks (assuming, of course, the gateway is connected to another network).

# Checking connectivity to a host

To check for a network path to a specific host, use the ping command. The ping command is a widely used TCP/IP tool that employs a series of Internet Control Message Protocol (ICMP, often pronounced as eye-comp) messages. ICMP provides for an Echo message to which every host responds. Using the ICMP messages and replies, ping can determine whether the other system is alive and then compute the round-trip delay in communicating with that system.

The following example shows how I run ping to see whether one of the systems on my network is alive:

```
ping 192.168.1.50
PING 192.168.1.50 (192.168.1.50): 56 data bytes
64 bytes from 192.168.1.50: icmp_seq=0 ttl=32 time=2.2 ms
64 bytes from 192.168.1.50: icmp_seq=1 ttl=32 time=1.2 ms
64 bytes from 192.168.1.50: icmp_seq=2 ttl=32 time=1.2 ms
64 bytes from 192.168.1.50: icmp_seq=3 ttl=32 time=0.8 ms

--- 192.168.1.50 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.8/1.3/2.2 ms
```

In Red Hat Linux, ping continues to run until you press Ctrl+C to stop it; then it displays summary statistics showing the typical time it takes to send a packet