
## Checking Out TCP/IP Networks

## /etc/nsswitch.conf

This file, known as the name service switch (NSS) file, specifies how services such as the name resolver library, NIS, NIS+, and local configuration files (such as /etc/hosts and /etc/shadow) interact.

NIS and NIS+ are network information services — another type of name-lookup service. Newer versions of the Linux kernel use the /etc/nsswitch.conf file to determine what takes precedence: a local configuration file, a service such as DNS (Domain Name Service), or NIS.

As an example, the following entries in the /etc/nsswitch.conf file say that the resolver first tries the /etc/hosts file, and then tries NIS+, and finally DNS:

```
hosts: files nisplus dns
```

You can find out more about the /etc/nsswitch.conf file by typing info "Name Service" (including the quotes) in a terminal window.

![](img/d9230b719dc0efd80851f363d8c6f571_349_0.png)

## Checking Out TCP/IP Networks

After you configure Ethernet and TCP/IP (whether during Fedora Core Installation or by running the Network Configuration tool later on), you can use various networking applications without problem. If you run into trouble, Fedora Core includes several tools to help you monitor and diagnose.

## Checking the network interfaces

Using the /sbin/ifconfig command to view the configured network interfaces (that is, to associate an IP address with a network). If you run ifconfig without arguments, the command displays information about current interfaces. The following is a typical invocation of result:

```
/sbin/ifconfig
eth0:Ethernet Haddr:00:08:74:e5:c1
       inet 192.168.0.2  broadcast:192.168.0.255  Mask:255.255.0
       inet6 fe80::24ff:fe60/64  scope=link
       MTU:1500  RX packets:9370  errors:0  dropped:0  overruns:0
       TX packets:7409  errors:0  dropped:0  overruns:0  collisions:0  txqueue:1000
eth1:Ethernet Haddr:00:02:20:8c:f5:c5
       inet 192.168.0.8  broadcast:192.168.0.255  Mask:255.255.255
       inet6 fe80::20ff:fe8c:c5/64  scope=link
       MTU:1500  RX packets:3403  errors:0  dropped:0  overruns:0
       TX packets:2255  errors:1  dropped:1  overruns:0  collisions:0  txqueue:1000
```

## Managing the Network: Checking TCP/IP Networks

This output shows that three interfaces — the loop interface (lo) and two Ethernet (eth0 and eth1) are currently active on this system. For each interface, you can see the IP address, as well as statistics on packets delivered and sent. If there is a dial-up link, you also see an item for the pp0 interface.

## Checking the IP routing table

The network configuration command, /sbin/route, provides status when it is run without command-line argument. If you're having trouble connecting to another host (that you specify with an IP address), check the routing table to see whether a gateway is specified. Then check the gateway's routing table to ensure that paths to an outside network appear in that table. A typical output from the /sbin/route command looks like the following:

```
/sbin/route
Kernel IP routing table Genmask Flags Ref Use Interface
192.168.0.0 * 255.255.0.0 U 0 0 eth0
192.168.0.0 * 255.255.0.0 U 0 0 eth1
127.0.0.0 * 255.0.0.0 U 0 0 lo
default 0.0.0.0 UG 0 0 eth0
```

As this routing table shows, the local uses the eth0 and eth1 interfaces, and the default gateway is the eth0 interface. The default gateway is a routing device that handles packets addressed to any network other than the one in which Fedora Core system resides. In this example, packets addressed to any network other than 192.168.0 are sent to the gateway — 192.168.0.1. The gateway forwards packets to other networks (assuming, of course, that the gateway is connected to another network, preferably the Internet).

## Checking connectivity to a host

To check for a network connection to a specific host, the ping command is a widely used TCP/IP tool that uses a series of Internet Control Message Protocol (ICMP, pronounced eye-comp) messages. ICMP provides an Echo message to which each host responds. The ICMP messages and replies can determine whether the other system is alive and can compute the round-trip delay in communicating with that system.

The following example shows how I run ping to see a system on my network is alive:

```
ping 192.168.0.1
```

Here is what command displays on my home network:

```
PING 192.168.0.1 (192.168.0.7) : 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=254 time=1.36ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=254 time=1.33ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=254 time=1.36ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=254 time=1.34ms

192.168.0.1 ping statistics
4 packets transmitted, 0% loss, time 302ms
r min/avg/max/dev=1.338/1.351/1.366/0.038
```

In Fedora Core, ping continues to run until you press Ctrl+C to stop; netstat shows all TCP connections — both active and the ones Fedora Core system is listening to (with no connection established yet). Netstat shows the status of the network. Netstat -a shows all TCP connections. Netstat -n shows the time.
