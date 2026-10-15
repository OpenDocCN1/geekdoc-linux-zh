# Using Hubs and Switches

If you're using a 10base-2 or 10base-5 Ethernet network, you'll link computers together in a bus topology, as described earlier in this chapter. 10base-T and 100base-T networks, however, normally operate in a star topology (depicted in Figure 1.3), using a device called a hub or a switch at the core of the star. A typical small network hub or switch is a plain box with several RJ-45 connectors and activity LEDs. Because your selection of a hub or switch can have important consequences for your overall networking experience, this section discusses these devices.

# NOTE

10base-2 and 10base-5 are older network technologies. Newer networks generally use 10base-T or 100base-T. I recommend 100base-T for all new installations, because it's the fastest type of Ethernet in common use at the end of 1999.

# Why Use a Hub or Switch?

First, if you're using 10base-2 or 10base-5 cabling, you don't need to—and indeed you can't—use a hub or switch. As a practical matter, then, you can ignore this question, unless you're considering upgrading your network to 100Mbps speeds, or even to changing to 10base-T.

10base-T and 100base-T cabling is designed for precisely two computers. You therefore can't use it as you do coaxial cable, in which you connect multiple computers to a single run of cable.

If you're using 10base-T or 100base-T networking cards and have only two computers to connect, you have the choice of using a hub, a switch, or a crossover cable. The crossover cable option is the simplest and least expensive in this situation because it's an ordinary Ethernet cable wired so you can directly connect the Ethernet ports on the two computers. For a two-computer network, this is quite adequate, and will save you the expense of a hub or switch. If you later decide to expand your network, you'll have to sacrifice the crossover cable, but nothing else.

If you're using 10base-T or 100base-T and want to connect three or more computers, you have little choice but to use a hub or switch. In theory, you could daisy chain computers by providing all but the endpoint machines with two NICs and configuring all the machines as routers; however, this would be far more effort than it's worth, and would probably cost more than buying a hub.