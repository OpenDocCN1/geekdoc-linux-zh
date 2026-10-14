**TIP** Clients require a network card, which can boot either via PXE or via Etherboot to allow initial booting for local media before piggyback booting from the network. More information can be found at http://rom-o-matic.net, where you can create bootable images for your network hardware. Etherboot is essentially a convenient way to emulate the PXE system on older hardware. Most newer motherboards and network cards come with PXE software on the chip.

# Technical Details of the LTSP Boot Process

A client machine is switched on. After the hardware is initialized, the network card looks for an IP address via the DHCP protocol. The LTSP server in most cases acts as the DHCP server to the local network and sends the client machine its IP address. Figure 5-7 shows a diagram of the LTSP booting process.

Once the network card has bound the IP address to itself, it makes a connection to the LTSP server and asks for the PXE configuration file. The LTSP server sends this file back to the client machine, which then makes a request for the kernel image. This is the base of the OS, which provides the client with all the hardware drivers required to communicate with the server.

![](bbox=[0.291, 0.581, 0.829, 0.88])