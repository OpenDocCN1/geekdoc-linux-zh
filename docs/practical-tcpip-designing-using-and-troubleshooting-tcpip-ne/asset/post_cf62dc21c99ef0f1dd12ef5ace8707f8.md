
or run by a single organization, and sites aren't connected to it in a hierarchical way. In fact, the connections form an untidy web or mesh as shown in Figure 5.1, so the routing system must be able to cope with this.

```
/* reach here only if not local to any of my interfaces */
else if (dest is in the IP address range for remote network-A)
    forward the packet towards dest via router-1
else if (dest is in the IP address range for remote network-B)
    forward the packet towards dest via router-2
```

Figure 5.2 Code a router uses to make decisions

Up to now we have implicitly assumed that a router is configured manually – that a network administrator tells this router about the various destinations and how to find them. This is the case for the internal networks in almost every small and medium-sized organization, and this chapter is devoted to configuring routing tables manually. For larger networks, and on the backbone of the Internet, something more sophisticated is needed, and in the Notes we look briefly at automatic routing protocols. These let routers find out from one another how to send to various destinations, and to inform one another when a connection breaks so that packets can be sent along a different path. This adaptive behavior is crucial for making the Internet resilient, allowing it to work even when individual components have failed.

But for now we'll consider only how routers are configured manually with their routing tables, which define both routes to other systems and, implicitly, which routers this machine can rely on to forward packets to other networks. Figure 5.3 shows a routing table from a Linux PC on a LAN, with three network cards. Ignore the detail for now – we'll explain it soon. Just notice that each entry consists of an IP address and netmask: as usual the combination specifies a range of IP addresses, and means "if I receive a packet with a destination address that belongs in this range, I will forward it to the gateway (router) specified." In other words, an entry is a *route* to a destination. Routing table entries are often referred to simply as "routes."

`alice$ route -n`

Kernel IP routing table

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.0.2.0 | 0.0.0.0 | 255.255.255.128 | U | 0 | 0 | 0 | eth0 |
| 192.168.168.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | 0 | eth1 |
| 10.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | 0 | eth2 |
| 0.0.0.0 | 192.0.2.29 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

Figure 5.3 Routing table from a Linux PC on a LAN

That's what routing tables are all about. You already know all the concepts involved. The hardest part to learn is how ranges are specified using netmasks, which you are an expert in by now! What complicates things is that the command syntax and output/GUI formats for setting and displaying routes are not very clear (i.e. it's not your fault, not yours, but the burden still falls on you). In the rest of this chapter we go on to look in detail at Linux and Windows routing tables and how to view them (and make sense of them), how to modify them, and how to troubleshoot them. (In the next chapter we apply all these techniques in practice, using them to set up test networks, and to divide a network into sub-nets.)

## 5.2 Routing table details – Linux

We start with Linux because it displays routing tables more simply than Windows. (Windows does the same thing but its display is more complicated.)

To display the routing table on this machine, use either of the commands:

`route -n`
`netstat -r -n`

which do exactly the same thing. (As usual, “-n” says to display IP addresses of networks and machines as numerics, not names.) **netstat** performs many network status functions; option “-r” selects the routing details display. Figure 5.4 shows the output for a typical LAN PC with one network interface. (“**Genmask**” means netmask. We don’t know why it’s called this – maybe to avoid calling it a sub-net mask, which would be even more confusing.)

```
alice% route -n
Kernel IP routing table
Destination    Gateway      Genmask         Flags Metric Ref    Use Iface
192.0.2.0      0.0.0.0      255.255.255.128 U     0     0      0 eth0
0.0.0.0        192.0.2.29   0.0.0.0         UG    0     0      0 eth0
```

**Figure 5.4** **route** output for a typical LAN PC with one network interface

> **Warning:** If you omit the “-n” by mistake, the information will be printed with names instead of numbers for gateways (see Figure 5.5) as long as your DNS is working correctly. But be warned: if your DNS (see Chapter 7) isn’t configured, **route** will still try the lookup, and will wait for about a minute and a half before giving up and printing the details numerically. Because this format is harder to interpret we won’t use it, even when the DNS is working.

```
alice% route
Kernel IP routing table
Destination     Gateway    Genmask         Flags Metric Ref    Use Iface
localnet        *          255.255.255.128 U     0     0      0 eth0
default        gate.uit.co.uk 0.0.0.0      UG    0     0      0 eth0
```

**Figure 5.5** **route**’s output if you omit “-n”

Here’s what the output means. When this machine receives a packet destined for IP address **pktdest**, TCP/IP executes the following for each line in the table:

```
if (**pktdest** is in the range specified by (**Destination**, **Genmask**))
    use this route
else
    move on to next line and try again
if no line matches **pktdest**, we can’t send the packet so report an error.
```

Then, if it has selected a route to use, it executes:

```
if (Gateway is 0.0.0.0)
/* means "we don't need a router; dest is directly connected. */
    send packet directly to pktdest, using ARP if necessary,
    via interface Iface
else
    send the packet to router Gateway for forwarding, via
    interface Iface
```

The comparison “if (Gateway is 0.0.0.0)” is confusing. It is merely Linux’s way of saying “this network is directly connected.” It is a notation only. The by-name listing in Figure 5.5 shows it as a “\*”, which is much clearer. Don’t be misled into thinking the 0.0.0.0 has a special technical meaning you can’t understand.

In Module 5.3 we’ll explain in detail how these routing table entries are created (although you already used them implicitly back in Chapter 3).

You can use the clever tool on our Web site to interpret Linux route -n or netstat -r -n command output, and print it in an operating-system-independent format.

Routes are ordered in the table from most specific down to least specific, and are selected in the same order, which is necessary if the default gateway route is to apply only when no other route is found.

### Linux routing table flags

Each entry in the Linux routing table listing can have zero or more one-letter “flags,” giving more information about the type of route it is.

| Flag | If present | If absent |
| --- | --- | --- |
| U | interface is Up, route is active | interface is down, making route inactive (but never shown: route is removed when interface goes down) |
| H | this route is for a single Host | this route is for a range of addresses (i.e. for a “network”) |
| G | destination is reachable via this Gateway (router) | destination is connected directly; send packets directly on Iface, using ARP if necessary |

The **H** flag is historical, and is compatible with other versions of UNIX. You don’t need it on Linux because the **Genmask** field tells you whether the address range contains only one address (a host) or many addresses (a “network” ).

## 5.3 Linux routing tables (1) – adding routes

The route command displays the current contents of the routing tables, as you've seen. You also use it to add or delete routes. It interacts directly with the kernel's tables, so changes you enter take effect immediately.

Using the route command is confusing and error-prone because of the number of options available and really horrible error messages, not because what you're doing is complicated. (It's just as bad on Windows too.) The route(8) manpage describes the command in detail, but doesn't show clearly which arguments apply to which sub-command (add, del, etc.) so we've spelt them out in the table below. When you're getting used to route, the best advice is to follow the command syntax from the table; you'll make fewer errors that way.

The "help" listing ("route -help -A inet") says you have to use "/" notation for net-masks; the manpage says you have to use full netmask notation. In fact you can use either, e.g. instead of **netmask 255.255.255.0**, append "/8" to the *destaddr* without any spaces on either side of the "/". You can also use the keyword *delete* (compatible with the Windows route command) instead of *del*.

### Adding routes

- add a route to a "network" (range of addresses)
```
route add -net destaddr netmask a.b.c.d gw routeraddr
```
The route will be displayed with the U and G flags. This is the type of route you will want to create most of the time.

- add a default gateway
```
route add default gw routeraddr
```

- add a route to a single host
```
route add -host destaddr gw routeraddr
```
The route will be displayed with the U, G, and H flags.

### Examples

To make the examples more concrete, assume we're adding routes on the PC shown in the little network in Figure 5.6. (The link to the Internet is dotted because the private 10.x.x.x addresses shown are not routable over the Internet.) To follow the examples on your own PC, it doesn't need to be connected to a network at all, and you certainly don't have to add the routers.

For the route commands to work, just ensure that your IP address is 10.1.1.11, netmask 255.255.255.0. "route -n" should then display output similar to Figure 5.7.

> Tip: after you enter each command, do a "route -n" to check the command has done what you expected.
