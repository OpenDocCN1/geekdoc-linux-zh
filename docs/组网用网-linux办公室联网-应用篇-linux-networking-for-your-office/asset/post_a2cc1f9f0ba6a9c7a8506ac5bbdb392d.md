
## Using Hubs and Switches

If you're using a 10base-2 or 10base-5 Ethernet network, you'll link computers together in a bus topology, as described earlier in this chapter. 10base-T and 100base-T networks, however, normally operate in a star topology (depicted in Figure 1.3), using a device called a hub or a switch at the core of the star. A typical small network hub or switch is a plain box with several RJ-45 connectors and activity LEDs. Because your selection of a hub or switch can have important consequences for your overall networking experience, this section discusses these devices.

### NOTE

10base-2 and 10base-5 are older network technologies. Newer networks generally use 10base-T or 100base-T. I recommend 100base-T for all new installations, because it's the fastest type of Ethernet in common use at the end of 1999.

## Why Use a Hub or Switch?

First, if you're using 10base-2 or 10base-5 cabling, you don't need to—and indeed you can't—use a hub or switch. As a practical matter, then, you can ignore this question, unless you're considering upgrading your network to 100Mbps speeds, or even to changing to 10base-T.

10base-T and 100base-T cabling is designed for precisely two computers. You therefore can't use it as you do coaxial cable, in which you connect multiple computers to a single run of cable.

If you're using 10base-T or 100base-T networking cards and have only two computers to connect, you have the choice of using a hub, a switch, or a crossover cable. The crossover cable option is the simplest and least expensive in this situation because it's an ordinary Ethernet cable wired so you can directly connect the Ethernet ports on the two computers. For a two-computer network, this is quite adequate, and will save you the expense of a hub or switch. If you later decide to expand your network, you'll have to sacrifice the crossover cable, but nothing else.

If you're using 10base-T or 100base-T and want to connect three or more computers, you have little choice but to use a hub or switch. In theory, you could daisy chain computers by providing all but the endpoint machines with two NICs and configuring all the machines as routers; however, this would be far more effort than it's worth, and would probably cost more than buying a hub.

Why the move from daisy-chainable coaxial cable to the more limited two-connection RJ-45 cable? Why make you buy this extra box? In a word, maintenance. A long run of coaxial cable is subject to problems such as breaks. For instance, suppose that an office uses 10base-2 cabling. If one computer's user drops a pen and crawls under the desk to find it, and if that person inadvertently hits the networking cable, pulling it loose from the computer, the network will end up broken into two parts, resulting in mysterious failures that may take some time to track down. If a 10base-T or 100base-T network was in place, by contrast, that same scenario would result in only one person's computer being affected—a problem that's much easier to diagnose.

An additional factor is that stringing cable like Christmas tree lights from one machine to another can result in some convoluted cable paths in some office layouts. While not guaranteed to always be better, a star topology can often produce saner and more flexible cable layouts.

Although I'm discussing Ethernet here, some other network technologies also use hubs, switches, or similar devices. Token Ring, for instance, uses a hub of sorts. The ring in a Token Ring network actually exists inside the Token Ring hub. This provides the advantages (and disadvantages) of a star topology to the ring topology used by Token Ring.

## The Difference Between Hubs and Switches

Hubs and switches fill very similar roles, but differ in important ways. If you've checked prices in stores, you'll have noted that switches are more expensive than hubs, assuming the same number of connectors. That's because switches are more complex and flexible devices. A hub is a pretty dumb device. When it receives an Ethernet packet from one device, it sends that packet back out to every other device attached to the hub. For instance, suppose you have a network with five computers connected to a single hub. When the computer called polk tries to communicate with the computer pierce, polk's packets do go to pierce, but they also go to the remaining three computers on the network, as shown in Figure 1.4. These computers won't attempt to process these packets because they recognize that the packets are for madison, but this blind relaying of messages to all systems does have negative consequences, as I describe shortly.

A switch, by contrast, is a bit smarter. It keeps within it a list of the Ethernet addresses of the computers it links together. Then, when it sees a packet coming in, it checks its destination address, and if it recognizes that address, the switch sends the packet only to that computer (as shown in Figure 1.5).
