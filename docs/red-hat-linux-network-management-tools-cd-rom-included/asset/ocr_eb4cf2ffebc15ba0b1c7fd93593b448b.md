cial broadcast message requesting the address of Node B to all devices on the network, as shown in Figure 3.19. All hosts receive the message, including Node B and Node C, but only Node B will respond with the correct physical address, as shown in Figure 3.20. The reason only Node B responds is because it examines the ARP packet and determines that its own IP address matches the target IP address that the requester is seeking.

![](bbox=[0.15, 0.25, 0.95, 0.525])

**Figure 3.19 ARP request.**

A sister function of ARP known as Reverse Address Resolution Protocol, or RARP, does the inverse; given a datalink address, it finds the corresponding IP address. RARP is primarily used when diskless workstations need to determine their IP addresses during system startup.

The term *broadcast* in the above example indicates a locally directed packet to all network devices on a particular LAN segment. Certain datalink protocols such as Ethernet provide the facility to transmit broadcast packets to all attached stations using a special destination address. With Ethernet, all 1s (or FFs in hexa-decimal) in the destination address is considered a broadcast. ARP assumes that the details of getting messages to each station will be handled directly by the datalink protocol.