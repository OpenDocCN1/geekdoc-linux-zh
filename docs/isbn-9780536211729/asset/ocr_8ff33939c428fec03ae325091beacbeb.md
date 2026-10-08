Source Address: Intermediary
Destination Address: Victim
Source Port: UDP 7 - charg

![](bbox=[0.165, 0.153, 0.803, 0.269])

Source Address: Victim
Destination Address: Intermediary
Source Port: UDP 7 - echo
Destination Port: UDP 19 - chargen

Figure 5.10 A UDP flood.

# FRAGMENTATION BOMBS

Different underlying network technologies (such as Ethernet, ATM, and token ring) define
different limits on the size of the Layer 2 frame. As a packet is passed from one router
to the next along the path from the source machine to the destination machine, network gate-
way routers might need to cut the packet into smaller pieces, called fragments, before pass-
ing them to the next network. In a legitimate fragmentation, the first fragment contains
the usual source and destination port numbers contained in the UDP or TCP transport
header. The following fragments do not.

For example, although the maximum theoretical packet length is 65,535 bytes, the max-\imum Ethernet frame size (Maximum Transmission Unit, or MTU) is 1,500 bytes.

When a packet is fragmented, intermediate routers do not reassemble the packet. The
packets are reassembled either at the destination host or by its adjacent router.

Because intermediate fragmentation is ultimately more costly than sending smaller,
nonfragmented packets, current systems often do MTU discovery with the target host or
t beginning of a connection. This is done by sending a packet with the Don't Fragment
option set in the IP header options for (the only legitimate use of the IP
options fields). If an intermediate router must fragment packet, it drops the packet and
returns an ICMP 3 error, fragmentation-required.

One type of fragmentation attack involves artificially very small packets.
One-byte packets crash some operating systems. Current operating systems usually test for
this condition.

Another use of small fragments is constructing the initial fragment so that the UDP or
TCP source and destination ports are contained in the second fragment. (All networks' MTU
sizes are large enough to carry a standard 40-byte IP and transport header.) Packet-filtering