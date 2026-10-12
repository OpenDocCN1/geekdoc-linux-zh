# A Dual-host No-NIC Network

The truly frugal can also “network” two Linux workstations using a null-modem or LPT cable and PPP, as shown in the PPP HOWTO at http://tldp.org/HOWTO/PPP-HOWTO/direct.html. Just connect two PCs running Linux together with a null-modem cable, and use the pppd daemon on each end. If one Linux host is connected to a network or has a dialup connection, that PC will become a gateway for the other host. You will need to use pppd’s *defaultroute* option on the serial-only host when connecting.

Each NIC has a unique address (the hardware address, known as Media Access Control, or MAC), which identifies that NIC. This address is six pairs of hexadecimal bits separated by colons (:). A MAC address looks similar to this: 00:60:08:8F:5A:D9. The hardware address is used by DHCP (see “DHCP” later in this chapter) to identify a specific host. It is also used by the *Address Resolution Protocol* (ARP) and *Reverse Address Resolution Protocol* (RARP) to map hosts to IP addresses.

This section covers some of the different types of NIC used to connect to your network.

# Token Ring

Token ring networking was developed by IBM. As the name implies, the network is set up in a ring. A single “token” is passed from host to host, indicating the receiving host’s “permission” to transmit data.

Token ring has a maximum transfer rate of 16Mbps (16 million bits per second). Unlike 10BASE-2 and 10BASE-5, token ring uses what is called *unshielded twisted pair* (UTP) cable. This cable looks a lot like the cable that connects your phone to the wall. Almost all token ring NICs are recognized by Linux.

# 10BASE-T

10BASE-T was the standard for a long time. A large number of networks still use it. 10BASE-T also uses UTP cable. Instead of being configured in a ring, 10BASE-T mostly uses a star architecture. In this architecture, the hosts all connect to a central location (usually a hub, which you learn about later in the section titled “Hubs”). All the data is sent to all hosts, but only the destination host takes action on individual packets. 10BASE-T has a transfer rate of 10Mbps.

10BASE-T has a maximum segment length of 100 meters. There are many manufacturers of 10BASE-T NICs, and most are recognized by Fedora.

# 100BASE-T

100BASE-T was popular around the turn of the millenium, keeping the same ease of administration as 10BASE-T while increasing the speed by a factor of 10. For most networks, the step from 10BASE-T to 100BASE-T is as simple as replacing NICs and hubs. Most 100BASE-T NICs and hubs can also handle 10BASE-T and can automatically detect which is in use. This allows for a gradual network upgrade and usually does not require rewiring your whole network. Nearly every known 100BASE-T NIC and most generic NICs are compatible with Linux, thanks to Donald Becker of http://www.scyld.com. 100BASE-T requires category 5 unshielded twisted pair cabling.