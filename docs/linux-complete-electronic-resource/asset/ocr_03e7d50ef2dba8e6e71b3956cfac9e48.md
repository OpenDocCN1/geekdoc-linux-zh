# Multicast

IP Multicast allows an arbitrary number of IP hosts on disparate IP networks to have IP datagrams simultaneously routed to them. This mechanism is exploited to provide Internet-wide "broadcast" material, such as audio and video transmissions and other novel applications.

**Kernel Compile Options:**

```
```
Networking options --->
  [*] TCP/IP networking
  ...
  [*] IP: multicasting
```
```

A suite of tools and some minor network configurations are required. Please check the Multcast-HOWTO (see `Multicast-HOWTO.html`) for more information on Multicast support in Linux.

# NAT—IP Network Address Translation

The IP Network Address Translation facility is pretty much the standardized big brother of the Linux IP Masquerade facility. It is specified in some detail in RFC-1631 at your nearest RFC archive. NAT provides features that IP Masquerade does not that make it eminently more suitable for use in corporate firewall router designs and larger-scale installations.

An alpha implementation of NAT for Linux 2.0.29 kernel has been developed by Michael Hasenstein <`Michael.Hasenstein@informatik.tu-chemnitz.de`>. Michael’s documentation and implementation are available from: Linux IP Network Address Web Page (see `http://www.csn.tu-chemnitz.de/HyperNews/get/linux-ip-nat.html`).

Newer Linux 2.1.* kernels also include some NAT functionality in the routing algorithm.

# Traffic Shaper—Changing Allowed Bandwidth

The traffic shaper is a driver that creates new interface devices, which are traffic-limited in a user-defined way. They rely on physical network devices for actual transmission and can be used as outgoing routed for network traffic.