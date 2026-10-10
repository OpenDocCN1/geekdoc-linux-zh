LAN can provide a focal point to workstations that could use Linux as a file server, a mail server, a print server, or a boot server. (Those features are described later in this book.)

Creating and configuring a LAN consists of these steps:

+   1. **Planning, getting, and setting up LAN hardware** — This entails choosing a network topology, purchasing the equipment you need, and installing it (adding cards and connecting wires or using wireless antennas).
+   2. **Configuring TCP/IP** — To use most of the networking applications and tools that come with Linux, you must have TCP/IP configured. TCP/IP lets you communicate not only with computers on your LAN, but with any computers that you can reach on your LAN, modem, or other network connection (particularly via the Internet).

# ### Planning, getting, and setting up LAN hardware

Even with a simple LAN, you must make some decisions about network topology (that is, how computers are connected). You must also make some decisions about network equipment (network interface cards, wires, switches, and so on).

The following paragraphs describe different types of network topologies you may be using:

+   * **Wired Ethernet LAN** — Most computers today on wired Ethernet networks use a star topology. In this arrangement, each computer contains a Network Interface Card (NIC) that connects with a cable to a central network switch or hub. The cabling is typically Category 5e or 6 (unshielded twisted pair) wiring with RJ-45 connectors. Other equipment, such as printers and fax machines, can also be connected to the switch in a star topology. Figure 14-4 is an example of a star topology.

# **Star Topology**

![](bbox=[0.3, 0.59, 0.7, 0.75])

**Figure 14-4:** In a star topology, machines on the network connect to a central switch or hub.

+   * **Wireless peer-to-peer** — In this topology, frames of data are broadcast to all nodes within range but are consumed only by the computers for which they are intended. This arrangement is useful if you are sharing file and print services among a group of client computers. Figure 14-5 shows an example of a peer-to-peer wireless LAN.