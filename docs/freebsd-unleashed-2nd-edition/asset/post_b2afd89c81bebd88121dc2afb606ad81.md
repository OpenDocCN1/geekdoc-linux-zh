
fitted to an adapter and a short crossover cable before it could talk to the smaller hub. Replacing the Ethernet cable with a long crossover cable was impractical, to say the least. Hence the uplink port was born—a port that allows a hub to be connected directly to another hub for which swapping out the cable for a crossover is not a viable option. Remember, though, that connecting two hubs' uplink ports together requires a crossover cable—and that's a configuration that rather defeats the purpose, in any case.

How do you tell whether an Ethernet cable is a straight-through or a crossover cable? It's pretty easy: Hold up the two ends of the cable next to each other. If the color sequences of the wires match, it's a straight-through cable. If some of the wires appear out of place, it's a crossover cable.

The pin-out for a straight-through cable is shown in Figure 21.6.

![](img/48eec858cce7dfb89da36a4d40b7daf3_518_0.png)

**FIGURE 21.6** Straight-through cable wiring diagram.

And to make a crossover cable, reverse the positions of pair 3 (wires 1/2) and pair 2 (wires 3/6), as shown in Figure 21.7, when crimping the second end.

![](img/48eec858cce7dfb89da36a4d40b7daf3_519_0.png)

**FIGURE 21.7** Crossover cable wiring diagram.

## Hubs

One end of the cable connects to your computer's Ethernet card; that much is clear. However, the other end needs to connect to something, too. Far more often than not, what it connects to is a hub.

Hubs are devices with multiple RJ-45 ports, usually between 4 and 24, to which you can connect as many Ethernet cables as there are ports. These cables can connect to computers, other hubs, switches, or other network components as necessary. Hubs range in cost from about $40 to several hundred dollars, depending on quality, number of ports, and the capability to operate simultaneously with 10base-T and 100base-TX devices. Many hubs can only do one of the two speeds; an auto-sensing hub (often referred to as N-Way) can do either speed but costs significantly more.

Hubs range in size from small boxes no larger than your hand (or smaller) to full 19-inch rack-mountable units, and all require a power source. Some hubs are even “managed,” meaning that you can telnet to them and configure each port's capabilities through a command-line interface. These hubs are naturally much more expensive than standalone hubs.

A hub is effectively a repeater, with all traffic appearing simultaneously on all ports, so a computer connected to one port on a hub will be able to see traffic to and from any other computer on the same hub. One port on a hub is usually reserved for uplink—a link to another hub, a switch, or a router higher up in the network hierarchy, as laid out earlier in Figure 21.1. This “uplink” port is usually wired so that a crossover cable is not needed between the hub and its next upstream device. This port and one of the standard ports on the hub may also be wired so that they’re mutually exclusive. A five-port hub might give you the option of hooking four computers together (ignoring the uplink port) or three computers to an upstream device (ignoring the fourth standard port). This behavior might be hard-wired, it might be controllable with a pushbutton or a DIP switch, it might auto-sense the polarity, or all the ports might be simultaneous usable. These are just some of the possible variations between different hubs.

Another matter that complicates the way hubs and other devices communicate with each other is the “duplex” mode in which they operate. In half-duplex mode, a host can only be “listening” or “talking” at one time. Full-duplex mode uses twice as many wires, enabling the host to “listen” and “talk” at the same time. Therefore, a 100Mbps Fast Ethernet link in full-duplex mode can transport up to 100Mbps on each direction simultaneously, whereas the same link in half-duplex mode can only do an aggregate total of 100Mbps in both directions.

Hubs can be thought of as a cheap replacement for switches, which we will discuss next. Because the cost of switches is dropping to nearly that of hubs, we may soon see the industry move entirely to switches, with hubs vanishing into obsolescence.

## Switches

A switch is another device that connects Ethernet devices together. A switch looks like a hub but tends to be more expensive and usually has fewer ports. It has multiple RJ-45 ports, it ranges from hand sized to rack sized, and the same companies that make hubs make switches, so it’s easy to mistake one for the other on store shelves. They even operate somewhat similarly—you can plug multiple devices into a switch, and a switch used in place of a hub in a network would usually give you what appears to be the same result. The difference between switches and hubs, however, is subtle yet crucial.

On a hub, all ports share the same internal wiring. All computers connected to the hub, either directly or through another hub, exist on what’s known as a collision domain. In a collision domain, a signal sent to one computer gets sent to all computers within the domain. It’s up to each computer’s Ethernet card to identify signals destined for that computer’s address and to discard all others.

A switch’s internal wiring is much more complex than a hub’s. Each port comprises its own collision domain, and hosts connected to one port can’t see any traffic destined for hosts on any of the other ports. Switches incorporate the software necessary to read each packet’s Ethernet header and destination MAC address (the unique identifier for each host's Ethernet card, as we will discuss later) and determine which port has the host that should get the packet. To make that determination, a switch stores an ARP cache, which is a lookup table of which hosts are on which ports. You can often confuse a switch by moving a computer from one port to another, so it may be necessary to power-cycle the switch in this circumstance (which clears most switches' ARP caches). Managed switches, like managed hubs, have complete command-line interfaces and configurability, with the attendant high price and complexity. There are even VLAN switches, which connect multiple LANs together using many different kinds of cabling mechanisms.

Because each port on a switch has its own collision domain, switched network traffic is able to take fuller advantage of the available network bandwidth. An eight-port, 100base-TX hub with all ports in use has to divide the available 100Mbps between the eight ports. If all eight ports are simultaneously trying to do bandwidth-intensive tasks and their aggregate bandwidth demand is greater than 100Mbps, “collisions” become more common. In a collision, two ports try to transmit or receive traffic at the same time, resulting in retransmissions at the physical link level and performance well below each host's logical share of the available 100Mbps. Switches alleviate this problem. Whereas a 100Mbps hub has 100Mbps of internal wiring in total, an eight-port switch has 800Mbps worth of wiring—the full bandwidth duplicated for every port. This is why switches tend to have fewer ports than hubs, and switches with many ports are quite expensive.

From a security standpoint, a fully switched network gives you the added benefit that machines in one collision domain can't see any traffic in any other collision domain. You can run a packet sniffer (such as tcpdump or EtherPeek) to put your Ethernet card into “promiscuous mode” (accepting all packets it sees regardless of whether they're destined for it) and spy on all other traffic within your collision domain. Switches allow you to separate these domains so that this isn't possible. This also protects your network from being overwhelmed by a single host that floods the network with an aggressive traffic flow, whether intentional or not, that uses all available bandwidth within the collision domain. Using switches rather than hubs, along with careful network planning, can greatly increase the network's reliability, security, and performance, thus making them worth the added cost.

Switches usually have no uplink ports. Occasionally, one or both ports have a pushbutton to select whether the ports need a straight-through or crossover cable. This is the case with some two-port switches, which serve purely as a filter to keep out irrelevant traffic. As a general rule, treat ports on a switch as hub-type devices and use crossover cables to connect one switch to another or a straight-through cable to connect a switch to a hub's uplink port. Most switches can auto-negotiate the speed and duplex mode of Ethernet cards, so you generally don't need to worry.

## Bridges

A bridge is another connecting device, in the class of hubs and switches, but it has a rather specialized purpose. It acts somewhat like a switch, but in a more complex way. A bridge is
