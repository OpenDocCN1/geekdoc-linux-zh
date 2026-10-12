
- 2. **ping**'s output reports the *round-trip time* (the time from when I sent the **ping** request to when I received the reply) so I can get a feel for the performance of the intervening network
- 3. **ping**'s time resolution varies on different machines and different operating systems, depending on the precision of your system clock. Try **pinging** for a variety of your machines and see what you get.

## ping command summary

The Linux and NT versions of **ping** use confusingly different flags for the same options. The important ones are summarized in Table 2.2. (Others are listed in your systems' respective manpages (online manual pages) or Help files, but you'll probably never need them.)

| | Linux | Windows-NT |
|---|---|---|
| **ping until ctrl-C terminates** | `ping host` | `ping -t host` |
| **send num requests** | `-c num` | `-n num` |
| **print host address as name** | *(default)* | `-a` |
| **print target address as number** | `-n` | *(default)* |
| **show final summary only** | `-q` | *(not applicable)* |
| **send request of size num bytes** | `-s num` | `-l num` |

## If ping doesn't get a reply

Apart from the general network problems that we cover in the troubleshooting Module 2.13, there are a couple of reasons why **ping** might not print anything:

- if the site is remote, it may be protected by a firewall that blocks **pings** (so that Bad People can't use **ping** to find out the addresses of your internal machines in preparation for an attack on your site)
- on Linux, you can disable responding to **pings** (see Notes on page 57 for details). We recommend you *don't* do this or you will confuse every administrator on your network (and probably yourself too when you forget what you've done)

> **Exercise:** when you boot your NT or Linux system, see where in the boot cycle it's first prepared to respond to **pings** it receives. Start a **ping** (which runs forever, by default) from a Linux system, or use **ping -t** from NT. If your network card or PCMCIA card has an "active" light, observe it (or the "link" light on your hub) to see when it becomes active. How does this relate to when the machine becomes **pingable**? You may find this information useful if you have boot problems on your system in the future.

Now we'll build a simple network and use the tools we've just covered.

## 2.7 Lab – building the simplest network possible: hubs and cabling

The simplest network we can have is two machines on a single Ethernet segment. UTP cabling is easy, flexible, and cheap. UTP hubs are easier to use than UTP switches when tracing packets.

We're now going to build the simplest possible network – two machines on a single Ethernet segment, as shown schematically in Figure 2.9. If you can, use Linux for one machine and Windows-NT for the other. It will take about five minutes to cable up the hardware (probably less than the time to find the spare hub) and another five or ten minutes to configure the software. We'll then perform experiments on it.

![](img/a2132b646d336d5f9a21102d6320e537_69_0.png)

## Cabling, hubs, and switches

The most commonly used cabling system nowadays is *UTP (unshielded twisted pair)*. This consists of several pairs of conductors, each pair twisted together, in a plastic outer casing, without any shielding around the pairs. By contrast, thin Ethernet ("thin-net") and thick Ethernet ("thicknet") have much thicker and more rigid coaxial, shielded cables, up to 10 or 11mm in diameter. On thin-net and thicknet, all the machines on the network attach to the single network cable. However, UTP uses a separate cable per machine, and all the cables are connected via *UTP hubs ("wiring hubs")* or *UTP switches* or a mixture of both. (We explain the difference between hubs and switches in the next module.)

We use UTP exclusively because:

- it's very flexible. You can easily run cable and sockets to where you need them, and it's very easy to build small test networks of a few PCs and hubs
- it's cheap – you can buy small UTP hubs for about US$20
- "link" indicator lights on hubs alert you to cabling problems without special diagnostic tools: if you connect a host to the hub and the link light doesn't come on, you've probably got a cable or similar problem (we say "probably" because the host and the network card must be up and running first)
- it's fast. By using the correct cable and hubs or switches, you can run 100 megabits/second Ethernet – ten times as fast as standard Ethernet but almost the same price
- it's easy to move, add, remove, or relocate computers in your network. This is very convenient when you're moving your sniffer machine to different points on the network to diagnose problems. UTP lets you keep a machine in its physical location but "cross-patch" it to connect into a different logical part of the network. If your sniffer has multiple network cards, you can, with suitable cross-patching, monitor local and remote parts of the network simultaneously from the one sniffer.

However, you can use any cabling system you like and everything we cover in this book still applies.

Using UTP, our simplest network is wired up physically as shown in Figure 2.10.

![](img/a2132b646d336d5f9a21102d6320e537_70_0.png)

**Figure 2.10** UTP cabling for a tiny network

We have shown a third machine, grayed-out in the diagram, running **tcpdump**. You can omit this if you run **tcpdump** on Alice or Bob instead. But we’ve found it easiest to keep **tcpdump** loaded on a dedicated laptop:

- it can be moved around at will, easily
- we know it works, whereas if you run **tcpdump** on Alice or Bob, you’re using a machine to diagnose itself, which will sometimes lead you into trouble.

(We use an ancient laptop as our day-to-day portable sniffer box. It’s the network administrator’s equivalent of a screwdriver – although we use **tcpdump** every day and only need a screwdriver once a week.)

Troubleshooting a network begins with the cabling. As we mentioned above, make sure when you connect the PCs to the hub that the “link” lights, which indicate that the connection has been correctly made, are on.

If you haven’t got a spare hub yet, you can connect Alice and Bob together directly using a *cross-over* UTP cable (Figure 2.11). Of course, with this configuration you can’t add a sniffer machine at all.

![](img/a2132b646d336d5f9a21102d6320e537_70_1.png)

**Figure 2.11** Connecting two machines using a cross-over UTP cable instead of a hub

> **Tip:** we always have our desktop PC connected to a hub that’s visible from where we sit. The “network activity” light on our port on the hub gives a good feel for what our machine is doing. It’s a cheap but immediate diagnostic indicator. For the same reason, we try to keep other network equipment (routers, firewalls, etc.) in easy view too.

### 2.8 Hubs v. switches

Appendix 3 explains the background of why hubs and switches are different, but here are the practical differences. In the context below a *port* is a connection point on a switch/hub that you connect a machine's Ethernet cable into.

**hub** – all the traffic on a port is visible on every other port and the bandwidth of the device is shared amongst all the ports (Figure 2.12). A heavy transfer from port X to Y will slow down a simultaneous transfer from A to B.

![](img/a2132b646d336d5f9a21102d6320e537_71_0.png)

![](img/a2132b646d336d5f9a21102d6320e537_71_1.png)

**switch** – traffic between two ports isn't visible on any other port. The full bandwidth of the device is available to every port (Figure 2.13). For example, if you have a 100Mb/s switch, you can transfer at 100Mb/s from port X to Y, and separately, at 100Mb/s from port A to B, and at 100Mb/s from Q to R as well. In fact, if your switch is *full-duplex*, you may even be able to transfer at 100Mb/s from B to A simultaneously with 100Mb from A to B. (When we upgraded from a 10Mb/s hub to a 100Mb/s switch, the time to update a particular file over the LAN reduced from 250 seconds to 11!)

On a switch, traffic between two ports A and B is visible only on ports A and B. On the network shown in Figure 2.14a, which uses a switch, if we run `tcpdump` on PC4, we won't see any of the PC2-to-PC5 traffic, even though our network card is in promiscuous mode, because the electrical signals just don't reach PC4.

![](img/a2132b646d336d5f9a21102d6320e537_71_2.png)
