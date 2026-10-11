
If you're building a 100Mbps network, I recommend that you purchase PCI NICs. Exceptions to this rule can involve:

- **Older computers**: If you have an old 80486 or earlier computer that doesn't support PCI, you naturally can't buy a PCI NIC for the computer. You might nonetheless want to seek out a 100Mbps-capable ISA NIC, because using a mix of 10- and 100Mbps boards can reduce your overall network's performance. Alternatively, use a 100Mbps NIC but make sure you use a switch rather than a hub to link your computers.
- **Low-speed interfaces**: Sometimes you need a single 10Mbps interface even on a 100Mbps network. For instance, if you use a Linux computer as a router between a network in your home or office and a cable or DSL modem, chances are the NIC that connects to the cable or DSL modem doesn't need 100Mbps speeds. For such a low-speed application, an ISA NIC is perfectly adequate. There's no reason to favor an ISA NIC for such an application, unless you're short on PCI slots.
- **Existing hardware**: If you have an existing ISA NIC and your situation doesn't require better speed than that card can provide, you might as well use it. PCI NICs can be quite inexpensive, though (as low as $15 or so from some vendors), so even a small reason to buy a PCI NIC can be enough to recommend doing so.

One other advantage of PCI NICs over ISA models is that the PCI devices tend to consume less in the way of CPU time than do the ISA NICs. Therefore, even when 10Mbps speeds are all you'll achieve, a PCI NIC is usually a better choice than an ISA model.

## Supported Linux Ethernet Chipsets

Like other expansion cards, Ethernet boards rely upon their chipsets to do most of the work. Linux drivers for these products are also written for particular chipsets. As a result, you might need to determine what chipset your Ethernet card uses before you can use it in Linux. Appendix A, “Linux Device Drivers,” covers this topic in detail. Fortunately, most Ethernet adapter manufacturers today include Linux drivers on their Web sites or on the floppy disks that come with their products. These drivers are typically just the normal Linux drivers for the chipset, but their inclusion makes it easy to determine which driver you need—you just examine the drivers included by the manufacturer and select the appropriate option during Linux installation.

In some cases, the driver included with the kernel might not support the latest version of a chipset. In these cases, you might need to obtain an updated driver or use the driver included with the board. Follow the directions that come with the updated driver to compile and install it.

Ethernet adapters are, as a class, one of the best-supported types of hardware in Linux. You can almost always find a driver for an Ethernet board. Some of the more popular boards and chipsets available today include:

- **3Com 3c59x and 3c905b series**: These chipsets are used in 3Com’s EtherLink XL series boards and on a few third-party products. They use the `3c59x` Linux driver.
- **DEC Tulip 21x4x series**: Digital Equipment Corporation (DEC) produced a popular series of Ethernet chipsets that were used on a large number of DEC and third-party products, many of which were quite inexpensive. When DEC folded, Intel bought the Tulip design, and a few products still ship with Tulip chips from Intel. These products use the Linux `tulip` driver.
- **Intel i82557/i82558 series**: These chipsets are used almost exclusively on Intel’s EtherExpress Pro/100B board. Some motherboards use this same chipset, and so work with the same Linux drivers, the `eepro100`.
- **NE2000 clones**: When ISA Ethernet cards were the rage, National Semiconductor produced a board called the *NE2000*. It became quite popular, and many manufacturers cloned it. Most of these clones work with the Linux `ne` driver. There are even NE2000 clones for the MCA (`ne2`) and PCI (`ne2k-pci`) busses.
- **RTL8129**: RealTek’s RTL8129 chipset has become fairly popular among low-cost boards from several manufacturers. It uses the `rtl8139` driver in Linux.
- **Tulip clones**: Several manufacturers, including PNIC and Macronix, have produced clones of the popular Tulip chipsets. Boards based on these products generally work well with the Linux `tulip` driver, and are quite popular because of their low cost. Some of these boards are new enough that they require an updated driver or kernel version 2.2.14 or later, however.
- **VIA Rhine**: VIA produces an Ethernet chipset known as the *Rhine* that’s been used in a number of low-cost PCI Ethernet boards. These products use the `via-rhine` driver.

As a general rule, any of these products works acceptably under Linux. If you need the best performance, though, you should probably favor an Intel, 3Com, or Tulip-based product, because these boards perform best under heavy network loads. NE2000 clones are particularly likely to produce poor throughput under heavy loads, and so should be avoided for servers.

You should not take the preceding list to be even remotely comprehensive. Many more products are available than I can list here, and most of them work well under Linux. For details, consult the Linux kernel configuration menus or the hardware compatibility list for your distribution.

## Non-Ethernet NICs

Some of the principles I've laid out for Ethernet adapters also apply to other network protocols. For instance, other types of NIC are available in PCI and ISA varieties, and the PCI variety is generally preferable, especially if the theoretical maximum network speed approaches or exceeds ISA's 5Mb/s (40Mbps).

As a general rule, I don't recommend you use anything but Ethernet for a new local network. Ethernet's popularity ensures that you'll get good prices on Ethernet hardware and be able to find support for any Ethernet networking problems you encounter. If you must hook your computer up to an existing network that uses another protocol, though, it might be simpler to use that protocol directly.

If you need to substantially expand an existing network, you have two choices:

- Expand the existing network using its own protocols. For instance, you might expand a 10-computer Token Ring network to 20 computers by using Token Ring directly in the new computers.
- Create two subnetworks, one of which uses the old protocol and one of which uses Ethernet. This approach is more complex, but has its advantages, such as higher speed if the old protocol is slower than 100Mbps. You'll need a dedicated router or a computer with one Ethernet and one alternative protocol NIC to link the two subnetworks.

You should probably consult a networking book or a networking consultant to help you decide which approach to take.

## Token Ring

IBM developed Token Ring technology to provide networking on small computers. There are two speeds of Token Ring available: 4Mbps and 16Mbps. Token Ring networks link their computers in a logical ring, as shown in Figure 17.2. Before it transmits data, a computer waits to receive a token from its neighbor. When the computer receives the token, it transmits the token along with a packet of data to its other neighbor. The neighbor computer then passes on the data, if required, and so it goes until the data reaches its intended recipient. Because only one computer at a time is allowed to transmit data, Token Ring networks don't suffer from collision problems, as can Ethernet networks.

In terms of hardware, Token Ring networks use a hub-like device and twisted-pair cables, so Token Ring hardware closely resembles that of 10BaseT or 100BaseT Ethernet. The Token Ring's ring is implemented inside the hub.

![](img/860d0c38bd76c9ded976e9d1e179ef25_483_0.png)

**FIGURE 17.2** *The closed loop of a Token Ring network lets the token cycle endlessly through the network.*

Linux includes support for several Token Ring adapters, under the Network device support, Token Ring devices kernel configuration option. Linux’s Token Ring support is much weaker than its support for Ethernet, however, so you should be sure to thoroughly investigate driver support for any Token Ring boards you might consider.

One particularly useful source of information for Token Ring users is the Linux Token Ring HOWTO document, which should come with your distribution. As of early 2000, this document had not been updated since 1998, however, so some of its information is geared towards 2.0.x-series and even earlier Linux kernels.

## LocalTalk

When Apple introduced its expensive LaserWriter printer in the mid-1980s, it needed some way to network the printer so that small offices could justify the printer’s high price. The result was a protocol called *AppleTalk*. That name originally applied to both the hardware and the software, but eventually the hardware acquired its own name: *LocalTalk*. Nonetheless, there are still occasional references to the hardware by the name *AppleTalk*.

By today’s standards, LocalTalk is quite primitive and slow. Its maximum speed is 2Mbps—one-fifth the speed of 10Mbps Ethernet, and one-fiftieth (1/50) the speed of modern 100Mbps Ethernet. The original LocalTalk cabling was a proprietary design and limited in length to 1,000 feet in a bus topology (described shortly). Although LocalTalk is an Apple technology, another company, Farallon, introduced a product called PhoneNET that allows LocalTalk to traverse ordinary telephone wires. PhoneNet also extends LocalTalk’s cabling range to 3,000 feet.
