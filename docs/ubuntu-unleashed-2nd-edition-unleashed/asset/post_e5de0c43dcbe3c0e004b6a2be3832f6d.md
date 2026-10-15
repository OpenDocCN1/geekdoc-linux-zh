
netmask would be 255.255.0.0; and for a Class C network, the netmask would be 255.255.255.0. Netmasks can also be used to deviate from the standard classes.

By using customized netmasks, you can subnet your network to fit your needs. For example, your network has a single Class C address. You have a need to subnet your network. Although this is not possible with a normal Class C subnet mask, you can change the mask to break your network into subnets. By changing the last octet to a number greater than zero, you can break the network into as many subnets as you need.

For more information on how to create customized subnet masks, see Day 6, "The Art of Subnet Masking," in Sams Teach Yourself TCP/IP Network Administration in 21 Days. That chapter goes into great detail on how to create custom netmasks and explains how to create an addressing cheat sheet for hosts on each subnet. You can also browse to the Linux Network Administrator's Guide and read about how to create subnets at http://www.tldp.org/LDP/nag2/index.html.

## Broadcast, Unicast, and Multicast Addressing

Information can get to systems through three types of addresses: unicast, multicast, and broadcast. Each type of address is used according to the purpose of the information being sent, as explained here:

- Unicast—Sends information to one specific host. Unicast addresses are used for Telnet, FTP, SSH, or any other information that needs to be shared in a one-to-one exchange of information. Although it is possible that any host on the subnet/network can see the information being passed, only one host is the intended recipient and will take action on the information being received.
- Multicasting—Broadcasts information to groups of computers sharing an application, such as a video conferencing client or online gaming application. All the machines participating in the conference or game require the same information at precisely the same time to be effective.
- Broadcasting—Transmits information to all the hosts on a network or subnet. Dynamic Host Configuration Protocol (DHCP) uses broadcast messages when the DHCP client looks for a DHCP server to get its network settings, and Reverse Address Resolution Protocol (RARP) uses broadcast messages for hardware address to IP address resolution. Broadcast messages use .255 in all the host octets of the network IP address. (10.2.255.255 will broadcast to every host in your Class B network.)

## Hardware Devices for Networking

As stated at the beginning of this chapter, networking is one of the strong points of the Linux operating system. This section covers the classes of devices used for basic networking. Note that this section talks about hardware devices, and not Linux networking devices, which are discussed in the section, "Using Network Configuration Tools."

## Network Interface Cards

A computer must have a network interface card (NIC) to connect to a network. Currently, there are several topologies (ways of connecting computers) for network connections. These topologies range from the old and mostly outdated 10BASE-2 to the much newer and popular wireless Wi-Fi or 802.11 networking.

## A Dual-Host No-NIC Network

The truly frugal can also "network" two Linux workstations using a null-modem or LPT cable and PPP as shown in the PPP HOWTO at http://tldp.org/HOWTO/PPP-HOWTO/direct.html. Just connect two PCs running Linux together with a null-modem cable, and use the pppd daemon on each end. If one Linux host is connected to a network or has a dial-up connection, that PC becomes a gateway for the other host. You have to use pppd's defaultroute option on the serial-only host when connecting.

Each NIC has a unique address (the hardware address, known as media access control, or MAC), which identifies that NIC. This address is six pairs of hexadecimal bits separated by colons (:). A MAC address looks similar to this: 00:60:08:8F:5A:D9. The hardware address is used by DHCP (see "Dynamic Host Configuration Protocol" later in this chapter) to identify a specific host. It is also used by the Address Resolution Protocol (ARP) and Reverse Address Resolution Protocol (RARP) to map hosts to IP addresses.

This section covers some of the different types of NIC used to connect to your network.

## Token Ring

Token ring networking was developed by IBM. As the name implies, the network is set up in a ring. A single "token" is passed from host to host, indicating the receiving host's permission to transmit data.

Token ring has a maximum transfer rate of 16Mbps (16 million bits per second). Unlike 10BASE-2 and 10BASE-5, token ring uses what is called unshielded twisted pair (UTP) cable. This cable looks a lot like the cable that connects your phone to the wall. Almost all token ring NICs are recognized by Linux.

## 10BASE-T

10BASE-T was the standard for a long time. A large number of networks still use it. 10BASE-T also uses UTP cable. Instead of being configured in a ring, 10BASE-T mostly uses a star architecture. In this architecture, the hosts all connect to a central location (usually a hub, which you learn about later in the section titled "Hubs and Switches"). All the data is sent to all hosts, but only the destination host takes action on individual packets. 10BASE-T has a transfer rate of 10Mbps.
