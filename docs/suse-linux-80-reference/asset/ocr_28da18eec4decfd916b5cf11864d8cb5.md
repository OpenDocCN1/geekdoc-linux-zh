Netmasks were conceived for the purpose of informing the host with the IP address 192.168.0.20 of the location of the host with the IP address 192.168.0.1.

# Netmasks and Routing

To put it simply, the netmask on a host with an IP address defines what is “internal” and what is “external”. Hosts located “internally” (professionals say, “in the same subnetwork”) respond directly. Hosts located “externally” (“not in the same subnetwork”) only respond via a gateway or router. Since every network interface can receive its own IP address, it can get quite complicated.

Before a network packet is sent, the following runs on the computer: the IP address is linked to the netmask via a logical AND, and the address of the sending host is likewise connected to the netmask via the logical AND. If there are several network interfaces available, normally all possible sender addresses will be verified.

The results of the AND links will be compared. If there are no discrepancies in this comparison, the destination, or receiving host, is located in the same subnetwork. Otherwise, it will have to be accessed via a gateway. That means that the more “1” bits are located in the netmask, the fewer hosts can be accessed directly and the more hosts can be reached via a gateway. Several examples are illustrated in Table 13.3 on the following page.

The netmasks appear once again — along with the IP addresses — in decimal form divided by periods. Since the netmask is also a 32-bit value, four number values are written next to each other. Which hosts are gateways or which address domains are accessible over which network interfaces must be entered in the user configurations.

To give another example: all machines connected with the same ethernet cable are usually located in the same subnetwork and are directly accessible. When the ethernet is divided by switches or bridges, these hosts can still be reached. However, the economical ethernet is no longer suitable for covering larger distances. You will then have to transfer the IP packets to another hardware (e.g. FDDI or ISDN). These devices are called routers or gateways. A Linux machine can, of course, also carry out this task. The respective option is referred to as ip_forwarding.

If a gateway has been configured, the IP packet will be sent to the appropriate gateway. This will then attempt to forward the packet in the same manner, from host to host, until it reaches the destination host or the packet’s TTL (time to live) has expired.