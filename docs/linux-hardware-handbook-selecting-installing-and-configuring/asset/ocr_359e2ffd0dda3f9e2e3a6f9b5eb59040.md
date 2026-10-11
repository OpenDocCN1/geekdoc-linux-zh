# Non-Ethernet NICs

Some of the principles I've laid out for Ethernet adapters also apply to other network proto-  cols. For instance, other types of NIC are available in PCI and ISA varieties, and the PCI vari-  ety is generally preferable, especially if the theoretical maximum network speed approaches or  exceeds ISA's 5Mb/s (40Mbps).

As a general rule, I don't recommend you use anything but Ethernet for a new local network.  Ethernet's popularity ensures that you'll get good prices on Ethernet hardware and be able to  find support for any Ethernet networking problems you encounter. If you must hook your com-  puter up to an existing network that uses another protocol, though, it might be simpler to use  that protocol directly.

If you need to substantially expand an existing network, you have two choices:

+   • Expand the existing network using its own protocols. For instance, you might expand a  10-computer Token Ring network to 20 computers by using Token Ring directly in the  new computers.

+   • Create two subnetworks, one of which uses the old protocol and one of which uses  Ethernet. This approach is more complex, but has its advantages, such as higher speed if  the old protocol is slower than 100Mbps. You'll need a dedicated router or a computer  with one Ethernet and one alternative protocol NIC to link the two subnetworks.

You should probably consult a networking book or a networking consultant to help you decide  which approach to take.

# Token Ring

IBM developed Token Ring technology to provide networking on small computers. There are  two speeds of Token Ring available: 4Mbps and 16Mbps. Token Ring networks link their com-  puters in a logical ring, as shown in Figure 17.2. Before it transmits data, a computer waits to  receive a token from its neighbor. When the computer receives the token, it transmits the token  along with a packet of data to its other neighbor. The neighbor computer then passes on the  data, if required, and so it goes until the data reaches its intended recipient. Because only one  computer at a time is allowed to transmit data, Token Ring networks don't suffer from collision  problems, as can Ethernet networks.

In terms of hardware, Token Ring networks use a hub-like device and twisted-pair cables, so  Token Ring hardware closely resembles that of 10BaseT or 100BaseT Ethernet. The Token  Ring's ring is implemented inside the hub.