Service. A single packet cannot be said to see a service contract. A flow of packets can see statistical properties with distributions such as interarrival and departure times, drop probabilities, reordering probabilities, erroring probabilities, and so on. The difference between distributions before and after service are the result of the scheduling discipline, combined possibly with the other traffic (especially true for best-effort and priority queuing). The state mathematics theory is such that we typically derive anything beyond mean and bounds (if they exist) for typical service classes and worst-case traffic. The Internet largely survives because FIFO and drop tail's amazing ability to survive many traffic arrival patterns, and under engineering. RED appears to improve this.

Session. An RSVP session defines one unicast or multicast data flow for which reservations are required. A session is identified by the destination address, transport layer protocol, and an optional (generalized) destination port.

Shape. Traffic may be within contract, but incur extra jitter due to bursts of other traffic when going through a switch. The jury is still out on whether one should reshape the traffic to its mean rate—typically, if a path has 2*bandwidth delay of buffering, then it can sustain any burstiness, however (and maximum) amount of burstiness—there is probably some statistical theory that could show this (e.g., diffusion model, or lattice gas occupancy theory), but it's beyond me now.

Shared style. A (reservation) style attribute; all reserved senders share the same reserved resources (see also distinct style).

Signal (see RSVP).

Soft state. Control state in hosts and routers that will expire if not refreshed within a specified amount of time.

Source. A host or router that can be identified by a unique unicast IP address.

Source routing. A technique for selecting a path out of many at the source—requires network to deliver choice to the source, and the source to be able to indicate choice in packet, or in signaling. Useful for policies, not for scaling.

SSH. Secure Shell.

State. Inurred from route, QoS, QoR, and signaled information.

SYN (synchronize). A bit set in the TCP header to indicate part of the three-way handshake to start a connection (by setting initial sequence numbers and other initial state).