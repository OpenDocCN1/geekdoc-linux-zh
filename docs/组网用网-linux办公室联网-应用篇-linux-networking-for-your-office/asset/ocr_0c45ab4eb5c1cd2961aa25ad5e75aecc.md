PCI cards are simpler to configure than ISA cards because they were designed with PnP in mind. Although all PCI cards are PnP devices, they don’t require separate configuration tools or explicit instructions on what resources to use; these details should be handled by the BIOS when the system boots. If you suspect you’re having problems with a PCI NIC because of resource conflicts, try using your system’s BIOS setup features to modify the way it assigns resources to PCI devices. Details vary substantially from one BIOS to another, but there’s generally a way to reserve specific resources for non-PCI devices or a selection of algorithms for assigning resources (for instance, assigning IRQs from low to high, from high to low, or in a specified order).

With both PCI and ISA boards, you’ll need to configure your Linux drivers appropriately. Before you can do that, however, you’ll need to know something about NIC chipsets.

# Ethernet Addresses

In order to identify themselves, Ethernet cards have unique six-byte addresses. These addresses are often, but not always, printed on a sticker attached to the card. Even when this is not the case, software can read the Ethernet address of a card. For instance, if you type /sbin/ifconfig at a Linux prompt, Linux responds with something like this:

```
eth0      Link encap:Ethernet  HWaddr 00:80:C8:F9:3B:BA
          inet addr:192.168.1.1  Bcast:192.168.1.255  Mask:255.255.255.0
          EtherTalk Phase 2 addr:65280/13
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:149265 errors:157 dropped:0 overruns:157 frame:0
          TX packets:186774 errors:3 dropped:0 overruns:3 carrier:0
          collisions:1132
```

The ifconfig command provides a great deal of information about the low-level network interfaces, but for the moment, consider only the first line of this output. The six hexadecimal values at the end of this line, labeled HWaddr, are the Ethernet address of this NIC.

The NIC’s Ethernet address is entirely separate from the numerical Internet address you may have encountered in the past, and which is described in Chapters 2 and 4. (This address is reported on the second line of ifconfig’s output, and is labeled inet addr:192.168.1.1 in the preceding example.) Ethernet boards use their hardware addresses to talk to each other, but not all computers on the Internet are connected via Ethernet, and not all Ethernet networks are connected to the Internet. One of the jobs of the TCP/IP stack, discussed in Chapter 2, is to link these two addresses in a meaningful way.