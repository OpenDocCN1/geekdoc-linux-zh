# Selecting the Hub or Switch That's Right for You

The main decisions you face in buying a hub or switch are whether you want a hub, a switch, or a hybrid device; and how many ports you need. Switches are, as I’ve said, superior to hubs in most respects, so if you find the price differential isn’t exorbitant, I recommend you buy a switch, or at least a hybrid device. For a small and low-bandwidth network, however, a hub might be adequate.

I recommend you buy a hub or switch with at least two ports more than you need in the near future. For instance, if you have three computers and expect to buy a fourth in a month or two, get a hub or switch with at least six ports. Doing so makes it less likely that you’ll need to replace or supplement your port in the near future.

Don’t feel compelled to purchase the same brand hub or switch that you used for any NICs on your network. Brand-to-brand incompatibilities between network components are extremely rare. My own home network, for instance, uses a Linksys hub and NICs (or built-in Ethernet ports) from Linksys, Kingston, NDC SOHOWare, D-Link, and Apple. These devices are all compatible with one another.

# Basic Linux Network Configuration

When you’ve got a network card, it’s time to configure Linux to use that card. Most of the effort involved in this configuration can be done when you install Linux—if your card is installed at that time, and if you know how your network is set up. If you add a card later, or if your network configuration changes, you might need to reconfigure all or some of Linux’s network settings. Although I can’t provide an absolutely complete set of directions for network configuration, I can provide an overview of the basics.

# Linux Kernel Configuration

As with many other hardware components, configuration of network cards begins with the kernel. There are three main kernel network configuration areas: Networking options, Network device support, and Ethernet (10 or 100Mbit). (Starting in the 2.3.x kernels, this final section has become a sub-section of the Network device support menu.) There are also a few menus relating to more obscure network devices, such as LocalTalk board drivers.

# Networking Options

The Networking options menu, shown in Figure 17.11, provides options for a variety of general-purpose networking features. For instance, it is here that you enable support for TCP/IP networking or other network stacks, such as AppleTalk. These options don’t relate to the low-level network hardware per se; instead, they cover the protocols that network utilities use.