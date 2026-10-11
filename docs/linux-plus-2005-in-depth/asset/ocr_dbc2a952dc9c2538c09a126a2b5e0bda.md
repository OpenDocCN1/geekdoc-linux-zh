> **NOTE**
> A computer uses its IP address and subnet mask to determine what network it is on. If two computers are on the same network, they can deliver packets directly to each other. If two computers are on different networks, they must use a router to communicate.

# Default Gateway

Typically, all computers on a LAN are configured with the same network ID and different host IDs. A LAN can connect to another LAN by means of a router, which has IP addresses for both LANs and can forward packets to and from each network. Each computer on a LAN can specify the IP address of a router in their TCP/IP configuration; any packets that are not destined for the local LAN are then sent to the router, which can then forward the packet to the appropriate network or to another router. The IP address of the network interface on the router to which you send packets is called the default gateway.

A router is often a dedicated hardware device from a vendor such as Cisco, D-Link, or Linksys. Other times, a router is actually a computer with multiple network cards. The one consistent feature of routers, regardless of the manufacturer, is that they can distinguish between different networks and move (or route) packets between them. A router has an IP address on every network to which it is attached. When a computer sends a packet to the default gateway for further delivery, the address of the router must be on the same network as the computer, as computers can send packets directly to devices only on their own network.

# TCP/IP Classes and Subnetting

IP addresses are divided into classes for management. The class of an IP address defines the default subnet mask of the device using that address. All of the IP address classes can be identified by the first octet of the address, as shown in Table 14-1.

Table 14-1 IP address classes

| Class | Subnet Mask | First Octet | Maximum Number of Networks | Maximum Number of Hosts | Example IP Address |
| :--- | :--- | :--- | :--- | :--- | :--- |
| A | 255.0.0.0 | 1–127 | 127 | 16,777,214 | 3.4.1.99 |
| B | 255.255.0.0 | 128–191 | 16,384 | 65,534 | 144.129.188.1 |
| C | 255.255.255.0 | 192–223 | 2,097,152 | 254 | 192.168.1.1 |
| D | N/A | 224–239 | N/A | N/A | 224.0.2.1 |
| E | N/A | 240–254 | N/A | N/A | N/A |