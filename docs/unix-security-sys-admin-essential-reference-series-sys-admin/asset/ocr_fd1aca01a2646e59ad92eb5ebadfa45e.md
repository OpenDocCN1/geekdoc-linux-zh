# Figure 12.1 A sample firewall implementation.

![](bbox=[0.17, 0.2, 0.9, 0.65])

# What Is a Firewall?

A firewall is a dedicated system situated between your internal network (sometimes called an intranet) and the Internet. The firewall system scrutinizes all offered network traffic and throws away or refuses any packets that would violate the integrity and security of the internal network.

The firewall is invisible to the users on the internal network. Internal workstations simply contact the firewall whenever they want access to the Internet. Users aren’t required to use special programs or contact special daemons running on the firewall. The firewall’s protective packet filtering is completely transparent.

# Dedicated Lines

My firewall connects to the Internet via a dial-up PPP connection. If your connection to the Internet runs via another interface, a 56k or ISDN packet connection for instance, you may use the following alternative. Use a dedicated router that connects to your Internet connection on one side, and a "normal" Ethernet on the other side. Then, equip your firewall with a second network card. Finally, connect your firewall, with a separate cable, to the router. The firewall will now transport packets between the two Ethernets. This Internet connection alternative is shown in Figure 12.1. Note that it is very important to use two physically separate network segments for this setup.