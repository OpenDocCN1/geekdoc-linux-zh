
A switch, by contrast, is smarter than a hub. A switch can examine the MAC addresses of the Ethernet frames it receives and forward the frames on to only the intended recipient. This situation is illustrated in Figure 17.10. The result is less network congestion and less chance of collision. For instance, if poik transfers data to pierre, as shown in Figure 17.10, while tyler transfers data to monroe, there need be no collision. This is despite the fact that both poik and tyler transmit at the same time—a situation which would cause a collision with a hub.

![](img/860d0c38bd76c9ded976e9d1e179ef25_493_0.png)

### Figure 17.10
A switch forwards data only to the intended recipient computer.

Switches offer the following additional benefits over hubs:

- Because of the one-to-one link allowed by a switch, computers linked by a switch can communicate using full duplex, which further increases throughput, particularly when two computers exchange data in both directions.
- The one-to-one link established by a switch lets two computers communicate at their fastest possible speed, even when that speed is faster than is supported by other computers attached to the switch. Hubs, by contrast, force all computers to run at the slowest supported speed. For instance, suppose madison in Figures 17.9 and 17.10 has a 10Mbps NIC, but all the other computers have 100Mbps NICs. In this case, poik and pierre can only transfer data at 10Mbps when a hub is used, whereas they can transfer data at 100Mbps when a switch is used.
- Because Ethernet frames normally go only to the recipient computer, switches make setting up a *sniffer* on one computer ineffective at retrieving data from other computers on the network. This feature is a major security benefit on networks on which individual computers might be compromised in one way or another. On the other hand, it can be a minus if you want to perform network diagnostics.

All in all, then, switches are superior devices. Why would anybody buy a hub? In a word, cost. Hubs have traditionally cost less than switches. Since 1998, though, the costs of hubs and switches have equalized somewhat. Hubs still cost less than switches, but the difference is less than it used to be.

If you have a small network (say, fewer than half a dozen computers) and don’t require the absolute best in speed, a hub can be an acceptable device. If you need the best performance possible, though, or if your network is large or hosts a lot of traffic, a switch is a better choice.

**TIP**
> Some devices have some hub-like and some switch-like characteristics. For instance, there are hubs that include two banks of connections, with switch-like communication between the two banks. Such devices can be very useful in reducing network traffic or supporting networks with a mix of 10- and 100Mbps NICs, without going for full switches. Such devices blur the line between hubs and switches, which complicates buying. You should be sure you get a full switch if that’s what you want, and not a hybrid device.

## Hub and Switch Features

Hubs and switches both vary in a number of features. A few additional features apply only to switches. Examples of features you should consider in switches or both devices include:

- **Speed** Ethernet hubs and switches are commonly available in 10Mbps and 100Mbps speeds. Most models sold today can automatically detect and use the appropriate speed, but some older models require you to flip a switch to set the appropriate speed. If you use a 10Mbps hub or switch, your network can’t run faster than this, even if you have category 5 cabling and 100Mbps NICs on all your computers.

**CAUTION**
> Some companies sell network kits that include a hub, two or three NICs, and appropriate cables. A few of these products advertise themselves as being 10/100Mbps kits, but they ship with 10Mbps hubs. If you buy a 10/100Mbps kit, be sure it includes a 100Mbps-capable hub as well as 100Mbps-capable NICs and category 5 cables.

- **Number of ports** The number of ports on a device determines the number of computers it can link. Few hubs or switches have fewer than four ports, but many support more—sometimes many more. Small home and office configurations seldom need more than a dozen or so ports, but large installations can need many more. Specialized rack-mount switches are often used for such configurations.
- **Uplink port** An uplink port allows you to link two hubs or switches together to increase their capacity or their geographic range. For instance, suppose you've got five computers in each of two rooms 40 feet apart, and you want to network all ten computers. You can buy two hubs or switches, each with an uplink port. Put one hub or switch in each room and run an Ethernet cable between them. When you connect the computers to their local hubs, the result is that all ten computers can see each other, as if they were connected to a single hub or switch. You can achieve a similar effect by using a crossover cable between ordinary ports on hubs or switches that aren't equipped with uplink ports.
- **LEDs** Most hubs and switches feature activity LEDs that help you diagnose problems. These LEDs don't vary a lot in their utility, but you might want to check for this feature in any event.
- **Noise** Some hubs, and especially some switches, have fans that can be noisy. Other devices have quieter fans or no fans at all.
- **Special features** Some devices include special features that can be of interest to those who use DSL or cable modems to connect to the Internet. These devices support the Dynamic Host Configuration Protocol (DHCP) or PPPoE protocols used by many cable and DSL providers. They can also support features similar to Linux's IP masquerading to let several computers share a single IP address. In fact, these devices are often more like routers than hubs or switches, and they're often sold as such. A router is a device that's more sophisticated than a switch, and it's used to link one network to another.
- **Throughput** Throughput is important for switches, but isn't normally a variable for hubs. Suppose you have a six-port 100Mbps switch. In theory, this switch can support three connections between pairs of computers, each of which can transfer up to 200Mbps of data (100Mbps in each direction), for 600Mbps total data throughput. In practice, most switches limit their throughput in one way or another, so you might not be able to achieve this level of performance. You should definitely check the throughput levels supported by any switch you buy, to ensure it's adequate for your anticipated needs.
- **Number of switched connections** As noted earlier, there are hybrid hub/switch devices available. To be sure of what you're buying, you should check that a device that advertises itself as a switch really is a full switch.

## Selecting the Hub or Switch That's Right for You

The main decisions you face in buying a hub or switch are whether you want a hub, a switch, or a hybrid device; and how many ports you need. Switches are, as I’ve said, superior to hubs in most respects, so if you find the price differential isn’t exorbitant, I recommend you buy a switch, or at least a hybrid device. For a small and low-bandwidth network, however, a hub might be adequate.

I recommend you buy a hub or switch with at least two ports more than you need in the near future. For instance, if you have three computers and expect to buy a fourth in a month or two, get a hub or switch with at least six ports. Doing so makes it less likely that you’ll need to replace or supplement your port in the near future.

Don’t feel compelled to purchase the same brand hub or switch that you used for any NICs on your network. Brand-to-brand incompatibilities between network components are extremely rare. My own home network, for instance, uses a Linksys hub and NICs (or built-in Ethernet ports) from Linksys, Kingston, NDC SOHOWare, D-Link, and Apple. These devices are all compatible with one another.

## Basic Linux Network Configuration

When you’ve got a network card, it’s time to configure Linux to use that card. Most of the effort involved in this configuration can be done when you install Linux—if your card is installed at that time, and if you know how your network is set up. If you add a card later, or if your network configuration changes, you might need to reconfigure all or some of Linux’s network settings. Although I can’t provide an absolutely complete set of directions for network configuration, I can provide an overview of the basics.

## Linux Kernel Configuration

As with many other hardware components, configuration of network cards begins with the kernel. There are three main kernel network configuration areas: Networking options, Network device support, and Ethernet (10 or 100Mbit). (Starting in the 2.3.x kernels, this final section has become a sub-section of the Network device support menu.) There are also a few menus relating to more obscure network devices, such as LocalTalk board drivers.

## Networking Options

The Networking options menu, shown in Figure 17.11, provides options for a variety of general-purpose networking features. For instance, it is here that you enable support for TCP/IP networking or other network stacks, such as AppleTalk. These options don’t relate to the low-level network hardware per se; instead, they cover the protocols that network utilities use.
