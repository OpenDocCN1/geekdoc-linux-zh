Local area networks (LANs) are confined to a relatively small area—a single computer facility, building, or campus. Today most LANs run over copper or fiberoptic (glass or plastic) cable, but other wireless technologies, such as infrared (similar to most television remote control devices) and radio wave (wireless, or Wi-Fi), are becoming more popular.

If its destination address is not on the local network, a packet must be passed on to another network by a router (page 376). A router may be a general-purpose computer or a special-purpose device attached to multiple networks to act as a gateway among them.

# ETHERNET

A Linux system connected to a LAN usually connects to a network using Ethernet. A typical Ethernet connection can support data transfer rates from 10 megabits per second to 1 gigabit per second, with further speed enhancements planned for the future. As a result of computer load, competing network traffic, and network overhead, file transfer rates on an Ethernet are always slower than the maximum, theoretical transfer rate.

+   Cables: An Ethernet network transfers data using copper or fiberoptic cable or wireless transmitters and receivers. Originally, each computer was attached to a thick coaxial cable (called thicknet) at tap points spaced at six-foot intervals along the cable. The thick cable was awkward to deal with, so other solutions, including a thinner coaxial cable called thinnet, or 10Base2,[^1] were developed. Today most Ethernet connections are either wireless or made over unshielded twisted pair (referred to as UTP, Category 5 [cat 5], Category 5e [cat 5e], Category 6 [cat 6], 10BaseT, or 100BaseT) wire—similar to the type of wire used for telephone lines and serial data communications.

+   Segment: A network segment is a part of a network in which all systems communicate using the same physical layer (layer 1) of the IP and OSI models (page 380).

+   Duplex: In half-duplex mode, packets travel in one direction at a time over the cable. In full-duplex mode, packets travel in both directions.

+   Hub: A hub (sometimes called a concentrator) is a device that connects systems so they are all part of one network segment and share the network bandwidth. Hubs work at the physical layer of the IP and OSI models (layer 1, page 380).

+   Switch: A switch connects network segments. A switch inspects each data packet and learns which devices are connected to which of its ports. The switch sorts packets and sends each packet only to the device it is intended for. Because a switch sends packets only to their destination devices, it can conserve network bandwidth and perform better than a hub. A switch may have buffers for holding and queueing packets. Switches work at the data link layer of the IP and OSI models (layer 2, page 380).

2. Versions of Ethernet are classified as XBaseY, where X is the data rate in megabits per second, Base means baseband (as opposed to radio frequency), and Y is the category of cabling.