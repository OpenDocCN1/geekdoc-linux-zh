later on. With the correct MAC address available, the system can prepare packets and send them out on the network via the Ethernet card.

You can use the arp command to display the ARP cache, a mapping of IP addresses to hardware addresses. The arp command is used mainly for troubleshooting network connectivity. Most entries in the ARP cache are dynamic and are discarded if not referenced within two minutes.

# Configuring Networking with Command-line Utilities

Most Linux distributions use a very similar set of commands and scripts to configure networking. In fact, the two core command line programs are the same on all versions of Linux: ifconfig and route. These commands are used by the script /etc/rc.d/init.d/network, which you learned about in Chapter 9, “Understanding System Initialization.” Here you learn about how those underlying networking utilities operate.

You used ifconfig in Chapter 7 to review the existing network configuration. The same utility is used to set up that configuration in the Linux kernel. This command is used by the system startup scripts at boot time, though you can use it to manually reconfigure the network if needed. The parameters used by ifconfig include, at a minimum, a network interface (such as eth0), the IP address assigned to the interface, and the network mask. These three pieces of information allow packets to be sent. A packet is a unit of data that the network card transmits. Additional parameters that can be configure using ifconfig include the broadcast address (an address that will send a packet to all computers on the same part of the network), the maximum transmission unit or MTU (the maximum size of packet that the interface supports), and various special features such as point-to-point connections and IPv6 addressing (which are not discussed in this chapter).

When you are working at a command line in Linux, you can enter the ifconfig command with an interface name such as eth0 to see the status of that interface:

```
$ ifconfig eth0

e th0      Link encap:Ethernet  HWaddr 00:01:02:76:FC:69
          inet addr:192.168.100.3  Bcast:192.168.100.255  Mask:255.255.255.0
          inet6 addr: fe80::201:2ff:fe76:fc69/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:16 errors:0 dropped:0 overruns:0 carrier:3
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 b)  TX bytes:3012 (2.9 Kb)
          Interrupt:11 Base address:0x1080
```

By specifying an interface such as eth0 in the ifconfig command, you can start an interface (“bring it up”) or stop it (“take it down”). To do this, you add up or down after the interface name. For example, to stop the Ethernet interface, enter this command:

```
# ifconfig eth0 down
```