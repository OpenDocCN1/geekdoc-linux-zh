# Hubs

One end of the cable connects to your computer's Ethernet card; that much is clear. However, the other end needs to connect to something, too; far more often than not, what it connects to is a hub.

Hubs are devices with multiple RJ-45 ports, usually between 4 and 24, to which you can connect as many Ethernet cables as there are ports. These cables can connect to computers, other hubs, switches, or other network components as necessary. Hubs range in cost from about $40 to several hundred dollars—depending on quality, number of ports, and the capability to operate simultaneously with 10base-T and 100base-TX devices. Many hubs can only do one or the other of the two popular speeds, and an auto-sensing hub (often referred to as N-Way) can cost significantly more. Hubs range in size from small boxes no larger than your hand to full 19-inch rack-mountable units, and all require a power source. Some hubs are even managed, meaning that you can telnet to them and configure each port's capabilities through a command-line interface. These hubs are naturally much more expensive than standalone hubs.

Hubs can be small standalone devices, as shown in Figure 12.5, or they can be sized to fit into a 19-inch networking rack.

FIGURE 12.5
Small five-port hub, with one Uplink port.

![](bbox=[0.42, 0.7, 0.88, 0.89])

A hub is effectively a repeater, with all traffic appearing simultaneously on all ports, so a computer connected to one port on a hub will be able to see traffic to and from any other computer on the same hub. One port on a hub is usually reserved for uplink—a link to another hub, a switch, or a router higher up in the network hierarchy, as laid out in