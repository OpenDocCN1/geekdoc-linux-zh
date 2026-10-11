
## Networking Transmission Issues

Hosts connect to a common network medium, sharing time and resources, so hardware identification suddenly can be an issue. Each packet needs a destination on a shared network. If the network connection is just two computers (a point-to-point network), the packet does not need a destination. The destination would be implied. However, the shared network needs a hardware address so that the network interface can select its messages from the myriad that zip by.

Ethernet LAN cards provide their own ID: the MAC, a six-byte ethernet address. When your computer sends a message, the networking subsystem divides the message into several frames, the smallest transmitted container. On an ethernet, each frame includes the source and destination MAC. Eventually the network associates the logical IP address with an actual physical (MAC) address. With the physical address, the LAN card listens for its address. When a matching address arrives, it opens its buffers and lets the message flow in.

The hardware issues focus on the technology of the physical communication channel. The next networking issue is moving the packet around the network. The packet faces many hazards that can corrupt or lose it entirely. Often the sender and receiver get little-to-no notification of a packet failure. Sometimes the receiver times out because it has not received a message from the sender when, in reality, the route between them may have severed.

Troubles regarding packets at the networking level typically involve problems with routing. Because the network changes while messages move from one place to another, knowing ahead of time what the symptoms can be can help you identify the problem and effect a solution.

Changes in network topology (or *propagation dynamics*) is a concern with even the most controlled network configurations. While it causes vary, it results in lost transmissions. One type of propagation dynamic is the network itself losing messages in transit. You may have experienced or heard about those networks in cubicles where someone moves his feet and shuts down someone else's cluster. Networks between computers change; connections between computers appear and disappear.

Another cause of propagation dynamics is excessive packet aging. As the packet propagates through a path, each node that forwards the packet tracks how old it is using a time-to-live (TTL) field. A packet expires when it exceeds the number of router hops it’s allowed. Each packet can get up to 255 hops; by default the value is 64 hops. Usually that is enough for your message to get where it’s destined to go.

The limit on the number of hops is important to keep the network from becoming overcrowded with long-dead packets. It’s easy for a packet that shows no tracking to cycle around endlessly. For example, suppose router A gets a message. A’s routing tables indicate that the best path is through B, so it sends the packet to B. Router B, however, lost its link, so it may send the packet back to A. Router A has no record of receiving the packet, so the packet bounces back and forth (until the TTL field expires or routers A and B synchronize their tables). The TTL field limits how long a packet goes around in a cycle.

Routing lists and host tables can become very large. Careful table management can help you avoid lengthy delays in calculating the best path to the destination.

While the complexity of the network is challenging, it is likewise complex to detect path loss, recovery, and cycles. Often, when a network segment disappears, cycles (or network loops) form that cause packets to age and die quickly. The network rarely notifies your sending and receiving hosts of the problem; the packets simply expire.

Sometimes pathway ambiguity can cause a packet in a message to be copied during transit (packet-mirroring or ghosting). This strange occurrence is undetectable unless each packet holds an ID or sequence number. Not only can the network duplicate information needlessly, but the network can also lose data through disappearing routers during a transmission or even packet corruption so that an error message never arrives back to the sender.

Packet loss happens all the time. Without accounting and acknowledgements, the originator may never determine whether the destination got the message.

Lastly, the segments may have router-data incompatibilities. Some routers or networks cannot support full 8-bit bytes or large packet sizes. The routers must convert the packets or return an error.

Fortunately, the networking issues arise only when you use lower-level protocols. If you don't have the time or want to face these challenges and you are satisfied with the slower throughputs, use the tested and proven high-level protocols. Most network applications use them. Once you have tested your algorithm with a high-level protocol, consider tuning your program for more performance with lower-level protocols. Then, when the dust of the project-building frenzy clears, hone and tune your algorithm to squeeze out more performance.

## Network to Operating System Interfacing

The network must be able to interface with the operating system for several reasons. To get its job done, the operating system handles the resources that the network subsystem needs, such as interrupts, ports, and memory. Also, while the networking subsystem manages the details of the network, it has to reside in the kernel for best performance.

The network-kernel interface is complex---especially if the kernel is not reentrant. Fortunately, the Linux kernel is now over the reentrancy hurdle and can handle the associated issues.

When a message arrives, the hardware sends an interrupt to the CPU to pick off the message. If the kernel (where the interrupt handler resides) is slightly late, another message may overrun the first message. This is especially true when the network card is put into **promiscuous mode** (accepting any and every message it hears). Chapter 3, “Different Types of Internet Packets,” first introduced the promiscuous mode.

Except for simulated networks like PPP, CPUs rarely work with the hardware networking interfaces directly. The CPU uses a coprocessor on the network interface card. The CPU loads the data into the network interface and instructs it to transmit. When done, the card raises an interrupt to the CPU. This instructs the kernel that the network card is again ready to accept another message. PPP on the other hand requires a lot more CPU interaction, but because the interface is much slower, it’s not as much of a burden as it could be.

A message queue holds the outgoing and incoming messages. When the kernel gets a notification that the card is ready for another frame, it takes the message directly from the message queue. If your program sends a message when the interface is not ready, the kernel places the request or message on the queue for later processing. The network is a limited resource; no two programs can access it at the same time. As a result, the operating system has to queue and process the requests one at a time.

Also, the kernel has to prepare each message for transmission, and it has to disassemble the incoming message for the receiver. The buffering subsystem tracks the constructed frames and readies them for the network or the client process (such as disk I/O).

Part of the process of packaging the message is assigning identification. Hardware identification (like the MAC) is clumsy and difficult to manage on a large network. So the network subsystem provides a logical identification (for example, the IP number).

Each packet needs the identification so that the operating system can quickly determine where to send it. IP numbering provides the network operating system a way of grouping computers together into subnetworks.

### Network to Program Interfacing

A main area of concern is how to interface the network to your program. Because network programming has so many angles and caveats, consider the specifics of each situation separately and then determine how they interrelate. This section discusses some of those issues.

The first issue is receiving and dealing with errors and exceptions. The operating system and your program must be able to receive and handle network errors or exceptions. Some errors and exceptions are asynchronous to the running program. C and Java can intercept them, but some languages cannot (for example, Pascal). So, as you consider how to write your application, keep in mind that not all languages lend themselves well to the demands of network programming.
