Here are some key points to note in Figure 1-2:

+   - Connect your DSL modem's data connection to the phone jack on a wall plate.
+   - Connect the DSL modem's Ethernet connection to the Ethernet card on your PC.
+   - When you connect other telephones or fax machines on the same phone line, install a *microfilter* between the wall plate and each of these devices.

![](bbox=[0.18, 0.32, 0.26, 0.42])

Because the same phone line carries both voice signals and DSL data, you need the microfilters to protect the DSL data from possible interference. You can buy them at electronic stores or from the DSL provider.

![](bbox=[0.18, 0.5, 0.26, 0.62])

When you connect your Red Hat Linux PC to the Internet using DSL, the connection is always on — and there is more potential for outsiders to break into the PC. You should make sure that the Red Hat Linux firewall setting is set at High Security. To configure the firewall settings, choose Main Menu→System Settings→Security Level from the GNOME desktop.

![](bbox=[0.18, 0.68, 0.26, 0.78])

There is another way to protect your Red Hat Linux system from intruders and, as an added bonus, share the high-speed connection with other PCs in a local area network (LAN). To do this, you need a router that can perform Network Address Translation (NAT). Such a *NAT router* translates multiple private Internet Protocol (IP) addresses from an internal LAN into a single public IP address, which makes it possible for all the internal LAN PCs to access the Internet.

If you also want to set up a local area network, you need an Ethernet hub to connect the other PCs to the network. Figure 1-3 shows a typical setup that connects a LAN to the Internet through a NAT router and a DSL modem.

Here are the points to note when setting up a connection like the one shown in Figure 1-3:

+   - You need a NAT router with two 10BaseT Ethernet ports (the 10BaseT port looks like a large phone jack, also known as an *RJ-45 jack*). Typically, one Ethernet port is labeled *Internet* (or External or WAN for wide-area network work), and the other one is labeled Local or LAN (for local area network).
+   - You also need an Ethernet hub. For a small home network, you can buy a 4- or 8-port Ethernet hub. Basically, you want a hub with as many ports as the number of PCs you intend to connect to your local area network.
+   - Connect the Ethernet port of the DSL modem to the Internet port of the NAT router, using a 10BaseT Ethernet cable (these look like phone wires with bigger RJ-45 jacks and are often labeled *Category 5* or *Cat 5* wire).