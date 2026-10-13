area network), and the other one is labeled **Local** or **LAN** (for *local area network*).

+   - You also need an Ethernet hub. For a small home network, you can buy a 4- or 8-port Ethernet hub. Basically, you want a hub with as many ports as the number of PCs you intend to connect to your local area network.
+   - Connect the Ethernet port of the DSL modem to the Internet port of the NAT router using a 10BaseT Ethernet cable. (The look like phone wires with bigger RJ-45 jacks and are often labeled Category 5 or Cat 5 wire.)
+   - Connect the Local Ethernet port of the NAT router to one of the ports on the Ethernet hub, using a 10BaseT Ethernet cable.
+   - Now connect each of the PCs to the Ethernet hub. (Of course, to do so, you must first have an Ethernet card installed and configured in each PC.)

![](bbox=[0.12, 0.384, 0.207, 0.454])

You can also buy a NAT router with a built-in 4- or 8-port Ethernet hub. With such a combined router/hub, you need only one box to set up a LAN and connect it to the Internet via a DSL modem. These boxes are typically sold under the name Cable/DSL router because they work with both DSL and a cable modem.

![](bbox=[0.12, 0.482, 0.207, 0.55])

DSL providers typically use a protocol known as PPP over Ethernet (PPPoE) to establish a connection between your PC and the equipment at the provider’s central office. PPPoE requires you to provide a username and password to establish the network connection over Ethernet. To set up your system for a PPPoE DSL connection, all you have to do is run YaST. (Choose Main Menu→System→YaST, click Network Devices on the left-hand window, and click DSL from the different network devices shown on the right-hand window.) YaST automatically detects the DSL modem and guides you through the configuration process.

# Connecting to the Internet
with a Cable Modem

Cable TV companies also offer high-speed Internet access over the same coaxial cable that carries television signals to your home. After the cable company installs the necessary equipment at its facility to send and receive digital data over the coaxial cables, customers can sign up for cable Internet service. You can then get high-speed Internet access over the same cable that delivers cable TV signals to your home.