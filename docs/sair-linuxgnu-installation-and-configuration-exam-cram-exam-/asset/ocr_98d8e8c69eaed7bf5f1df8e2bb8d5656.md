![](bbox=[0.17, 0.08, 0.27, 0.2])

Plug-and-Play BIOSes also set the communication ports (IRQ, DMA, I/O, shared memory address) used by each component.

However, Plug-and-Play BIOSes are not perfect. The ports that are assigned in Linux may still conflict. You may need to set the ports manually. If you have a lot of conflicts, you may even have to deactivate Plug-and-Play in your BIOS.

# Solutions

When you have a conflict, you need to assign different ports. You can make changes with commands, such as isapnp or ifconfig. In some cases, you can even use your Linux distribution's GUI configuration tools; I've used Red Hat's LinuxConf and S.u.S.E.'s YaST with some degree of success in this area.

Sometimes, you can change the port or address on the card itself. Some newer cards come with driver floppies that change the software embedded in the card. If you don't have the floppy available, you may be able to download the program from the manufacturer's Web site.

Alternately, some older adapter cards work with jumpers, which are connectors on the card that you can physically remove and install on different combinations of metal pins. The port or memory address used by your card depends on the pins connected by the jumper.

> Note: If you have to work with components inside your computer, take precautions. Turn off your computer before taking it apart. Be sure to touch some large metal object (such as a metal computer case) to dissipate static electricity before you touch anything inside your computer. Be gentle when you remove or install anything (cards, chips, and so on).

# Memory

The amount of RAM that you need for Linux depends on what you want to do with your computer. Linux doesn't require a lot of RAM. The Linux kernel needs about 1MB of space. The programs for which you need to set up a CLI require another 2MB to 3MB. In other words, if you're just setting up a Linux computer as a network firewall, 4MB of RAM may be enough.

The following sections describe four possible installation scenarios for Linux.

# Network Firewall

You can set up a Linux computer as a dedicated firewall to protect the rest of your network. A properly installed firewall is the only path between your local area