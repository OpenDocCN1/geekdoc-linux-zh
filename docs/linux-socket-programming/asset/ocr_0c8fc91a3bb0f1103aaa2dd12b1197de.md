Data frame repeaters accept all network messages and pass them on to a new segment of the network. Data repeaters are dumb in that they do not select from packet to packet and ignore the hardware identifications. A data repeater has less programming intelligence than a typical repeater, which selectively permits packets between segments and resides in the Physical layer. Use a data repeater to extend the network length and amplify the attenuated signal.

Lastly, some ethernet adapters now include a checksum or CRC of their own to perform data validation checks. If CRC finds an error, the card flags the data as suspect for the Datalink layer to fix. This may give you a little more confidence in the datagram protocols.

Other physical networks may have other mechanisms. For example, the PPP connection may include a parity (most don't). FDDI has checksumming or CRCs. Some obscure radio protocols simply send each character twice.

# Layer 2: Datalink

The Datalink layer rests on the Physical layer. The primary role of the Datalink layer is to provide data transfer from host to host. It packages messages into frames for the hardware. It checks for and tries to correct transmission errors. If the hardware does not support checksums or CRCs, the Datalink layer does the calculations itself.

The Datalink layer interfaces the kernel to the network hardware. Typically, the Datalink layer is a network driver that resides in the kernel. The driver uses a uniform interface so that the kernel can work blindly with vastly different technologies.

This layer prepares the data frames for transmission and disassembles received messages. The driver waits for interrupts that indicate a message was sent or a message was received. When it gets a message-sent notification, the Datalink driver loads the next frame to send.

The Datalink works closely with the buffering subsystem of the kernel. Most of the time, it only needs 10–60KB of system RAM. Linux’s kernel configuration lets you define the size of the buffering and frame beyond 1MB for very fast transfers (100MB/s or higher), if you have enough memory. This is useful for very high-speed connections that may receive large frames or high throughput. To use this feature, you may have to recompile the kernel, because many Linux distributions do not enable it.

Network bridges reside in the Datalink layer. The Linux kernel’s bridge option is still experimental at the time of this writing. If you want to experiment with it, you may have to reconfigure and compile the kernel to include the drivers.

The Network layer rests on top of the Datalink layer and provides address resolution and routing.

# Layer 3: Network

The Network layer rests on top of the Datalink layer. Its primary function is to work with the routing tables, routers, and gateways to find the destination host. In a non-routed network, this layer is essentially inactive.

The Network layer provides a uniform addressing mechanism for heterogeneous networks. If, for example, you have two physical networks such as AppleTalk and Ethernet, this layer bridges them using a frame translation.