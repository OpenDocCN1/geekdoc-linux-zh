![](bbox=[0.18, 0.12, 0.39, 0.26])

Chapter 8, “Configuring Basic Networking,” introduced the topic of network configuration, but it covered only the basics of network configuration and diagnostics. This chapter continues this introduction to networking by tackling several important topics. These include additional information on router configuration, network ports, and packet filtering (a security tool that enables you to drop, redirect, or modify packets based on a wide variety of criteria). These topics are particularly important if you want to configure a Linux system as a router—a system that directs data between two networks.

This chapter also covers a couple of important classes of network servers and clients: remote login tools and the Common Unix Printing System (CUPS) utility for printing. Both ordinary users and system administrators can use remote network access. CUPS is used for printing even on Linux systems with no regular network connections, but CUPS really shines on a network, since it enables seamless sharing of printers. Chapter 10, “Configuring Network Servers I,” and Chapter 11, “Configuring Network Servers II,” continue the examination of Linux networking by delving into a number of additional network server packages.

> Objective 4.3 is covered partly in this chapter and partly in Chapter 8.

# ## Routing Between Networks

Chapter 8 provided information on router configuration, including the use of the route command to tell your computer about the local networks to which it’s attached and how to direct network traffic to computers on other networks.

A typical configuration involves just one local network and one router or gateway system; however, Linux can support much more advanced configurations. For instance, suppose a computer has two network cards, each of which is connected to a different network. The routing table on such a computer might resemble the following, as reported by route:

```
```
$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
172.24.21.0     0.0.0.0         255.255.255.0   U     0       0      0     eth0
192.168.1.0     0.0.0.0         255.255.255.0   U     0       0      0     eth1
0.0.0.0         192.168.1.254   0.0.0.0         UG    100     0      0     eth1
```

```