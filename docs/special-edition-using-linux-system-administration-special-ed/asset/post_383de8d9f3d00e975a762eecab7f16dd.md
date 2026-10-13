
Notice the use of the `-host` option instead of `-net` when specifying a static route for a host.

The route command is also discussed in Chapter 13.

## PREPACKAGED ROUTING DISTRIBUTIONS

Although any Linux distribution can be used to create a Linux-based router, this is often inefficient. For instance, the complete Red Hat Linux distribution includes a large amount of extra software and kernel modules, which means it requires a larger memory and disk footprint than a Linux router necessarily requires. If you want to run a Linux system strictly as a router, distributions are available that even fit on a floppy disk that can create a Linux router with limited memory and no hard disk.

The advantages of a floppy-based approach to creating a Linux router include the following:

- No need to configure the router for additional security by turning off all the extra network services that typically run in a standard distribution.
- No need to recompile the Linux kernel with support for IP forwarding.
- Easy disaster recovery because you can keep multiple copies of the router diskette on hand and swap them if one fails.
- No need to perform backups. Everything is maintained on a single floppy disk that is easily duplicated and stored for future use.

Several single floppy disk distributions for creating a Linux-based router and firewall are available, including the following:

- **Linux Router Project (www.linuxrouter.org):** This is the leading single floppy disk router distribution. This distribution can be used to build Ethernet routers, ISDN routers, remote access servers, thin clients, firewalls, and network appliances.
- **floppyfw (http://www.zelow.no/floppyfw/):** `floppyfw` is a Linux-based static router with network address translation (IP Masquerading) and packet-filtering capabilities. It cannot be used for sophisticated firewalls but is perfect for a quick-and-dirty packet-filtering router and firewall.
- **MuLinux (http://sunsite.auc.dk/mulinux/):** MuLinux is a floppy disk-based Linux distribution that, although not specifically focused on router creation, is ideal for that purpose. Depending on how you configure it, MuLinux can include NFS booting for X-terminal clients, DHCP support, email processing and reading, Samba support, sound support, and X Windows capabilities.
- **DLX (http://www.wien.at/usr/h93/h9301726/dlx.html):** DLX is a single floppy disk distribution for general purpose use. It includes network support and parallel port zip drive support. It can be used for building a router and is ideal for network troubleshooting.

![](img/6c13bcf02a08ad7923caab46f051d96a_313_0.png)

## CREATING A LAN-TO-LAN ROUTER WITH LINUX

To illustrate the creation of a basic Linux router, implement a router for directly connecting two class C networks: `10.10.10.0` and `10.10.20.0`. Figure 15.3 outlines the network configuration you want to implement.

**Figure 15.3**  
Two networks connected by a router.

![](img/6c13bcf02a08ad7923caab46f051d96a_314_0.png)

You can create a LAN-to-LAN router for this network topology using a standard Linux distribution as follows:

1. Check whether IP forwarding is compiled into your kernel, and if not, compile and install it. This process is described earlier in this chapter in the “Kernel Modules for Routing” section.

2. Install two network cards in your system and make sure they are running properly as outlined in Chapter 13 in the “Configuring Multi-Homed Hosts” section.

3. Configure `eth0` to attach to the `10.10.10.0` network as outlined in Chapter 13. Presume that the IP address of the router on the `10.10.10.0` network is `10.10.10.1`.

4. Configure `eth1` to attach to the `10.10.20.0` network as outlined in Chapter 13. Presume that the IP address of the router on the `10.10.20.0` network is `10.10.20.1`.

5. Check your routing table using the `route` command. You should have static routes to both networks through the appropriate interface as follows:

   ```text
   10.10.10.0    *    255.255.255.0    U    0    0    0    eth0
   10.10.20.0    *    255.255.255.0    U    0    0    0    eth1
   ```

6. If the static route to the `10.10.10.0` network is missing, use the following command to create the route:

   ```bash
   # /sbin/route add -net 10.10.10.0/24 dev eth0
   ```

7. If the static route to the `10.10.20.0` network is missing, use the following command to create the route:

   ```bash
   # /sbin/route add -net 10.10.20.0/24 dev eth1
   ```

Hosts on the `10.10.10.0` network need to be configured to use the router at `10.10.10.1` as their default gateway.

```bash
# /sbin/route default gw 10.10.10.1 dev eth0
```

Similarly, hosts on the `10.10.20.0` network need to be configured to use the router at `10.10.20.1` as their default gateway:

```bash
# /sbin/route default gw 10.10.20.1 dev eth0
```

When your router is running, you need to consider security on the router:

- Should the router accept remote logins through telnet or rsh for remote management? If not, enable remote management with ssh or only allow management at the console.
- The router should not be part of your NIS domain to prevent regular user accounts from logging in to the router.
- Only the minimum number of user accounts in addition to system accounts and the root account should exist on the router.
- All unnecessary network services should be disabled on the router, including sendmail, FTP, Telnet, NFS, Samba, LPD. Not running unneeded services helps prevent unauthorized access to the router.
- Consult Chapter 18, “General Security Issues,” and Chapter 19, “Linux and Firewalls,” for guidance about securing your Linux router system. The same rules that apply to keeping a firewall secure apply to keeping a router secure.

## DYNAMIC ROUTING

The preceding sections have discussed static routing. However, static routing suffers from a major drawback: the daunting task of maintaining routes in a changing network environment. Routing protocols provide a mechanism for handling both simple and complex routing environments.

There are a variety of routing protocols, and they all basically perform the same function: They determine the best route to a destination host or network. In this chapter, you will look at two such protocols: the Routing Information Protocol (RIP) and the Open Shortest Path First (OSPF) protocol. You will also consider two daemons used for deploying these protocols: routed, which implements RIP, and gated, which supports RIP, OSPF, and other routing protocols.

## TYPES OF ROUTING PROTOCOLS

There are two types of routing protocols: interior protocols and exterior protocols. An interior routing protocol is used inside an independent network system. An independent network system is called an autonomous system (AS). RIP and OSPF are widely used interior routing protocols.

Exterior routing protocols are used to exchange routing information between independent networks or autonomous systems. The Border Gateway Protocol (BGP) and the Exterior Gateway Protocol (EGP) are examples of exterior routing protocols. Discussion of exterior routing protocols is beyond the scope of this book. BGP is the newer protocol that has evolved out of experience gained from EGP. For more information on BGP, refer to the following RFCs:

- RFC-1771, “A Border Gateway Protocol 4 (BGP-4)”
- RFC-1773, “Experience with the BGP-4 Protocol”
- RFC-1774, “BGP-4 Protocol Analysis”
- RFC-1965, “Autonomous System Confederations for BGP”
- RFC-1966, “BGP Route Reflection an alternative to full mesh IBGP”
- RFC-1997, “BGP Communities Attribute”
- RFC-1998, “An Application of the BGP Community Attribute”
- RFC-2283, “Multiprotocol Extensions for BGP-4”
- RFC-2385, “Protection of BGP Sessions via the TCP MD5 Signature Option”
- RFC-2439, “BGP Route Flap Dampening”
- RFC-2545, “Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain”
- RFC-2547, “BGP/MPLS VPNs”

## ROUTING INFORMATION PROTOCOL

The Routing Information Protocol (RIP) is one of the most commonly used interior gateway protocols. RIP classifies routers and hosts as active and passive. Active routers advertise their routes to others, whereas passive routers listen and update their routes based on advertisements but do not advertise their own routing tables to anyone. Typically, routers run RIP in active mode, whereas hosts run it in passive mode.

Active mode RIP routers broadcast updates at a set interval (normally every 30 seconds). RIP updates consist of a network IP address and an integer distance to that network. The distance to a network is based on the number of gateways that must be traversed to reach that network, and it is referred to as the *hop count*. Directly connected networks have a hop count of one, which is analogous to a RIP metric of one. Using hop counts to calculate the best route does not always produce the best result. For example, a route with a higher hop count crossing several fast-Ethernet segments might be much faster than a route with a lower hop count across a WAN connection over a slow-speed serial line.

To correct this situation, many RIP routers advertise artificially high hop counts for slow links. The maximum hop count is 15, beyond which the network is considered unreachable. In general, routing updates are sent out every 30 seconds. If a gateway is not heard from for more than 180 seconds, it is considered dead, and all routes using this gateway are deleted from the routing table. Many versions of UNIX run a RIP routing daemon called routed to implement RIP on their networks.
