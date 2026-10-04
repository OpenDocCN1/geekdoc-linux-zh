# Connecting Your LAN to the Internet 305

5. Click Forward, and then Apply to complete the Ethernet setup.

You're back in the Network Configuration dialog box (refer to Figure 2-3).

6. Select the eth0 device and then click Activate to turn the Ethernet network on.

If you are running a private network, you may use IP addresses in the 192.168.0.0 to 192.168.255.255 range (Other ranges of addresses are reserved for private networks, but this range suffices for most needs.)

![](bbox=[0.135, 0.226, 0.203, 0.296])

# Connecting Your LAN to the Internet

If you have a LAN with several PCs, you can connect the entire LAN to the Internet by using DSL or cable modem. Basically, you can share the highpeed DSL or cable modem connection with all the PCs in the LAN.

Chapter 1 of this minibook, I explain how to set up DSL or cable modem. In this section, I briefly explain how to connect a LAN to the Internet so all the PCs can access the Internet.

The most convenient way to connect a LAN to the Internet via DSL or cable modem is to buy a hardware device called DSL/Cable Modem NAT Router with a 4- or 8-port router can translate private IP addresses into a single externally known IP address. The Ethernet hub part appears to you a number of RJ-45 Ethernet ports where you can connect the PCs to set up a LAN. In other words, you need only one extra box besides the DSL or cable modem.

Figure 2-5 shows how you might connect your LAN to the Internet through a NAT router with a built-in Ethernet hub. Of course, you need a DSL or cable modem hookup to work (and you have to sign up with the phone company for DSL service or with the cable provider for Internet service).

When you connect a LAN to the Internet, the NAT router acts as a gateway for your LAN. The NAT router also dynamically provides IP addresses to the PCs in your LAN. Therefore, on each PC, you have to set up the networking options to obtain the IP address dynamically.

Book IV
Chapter 2
Setting Up a Local
Area Network