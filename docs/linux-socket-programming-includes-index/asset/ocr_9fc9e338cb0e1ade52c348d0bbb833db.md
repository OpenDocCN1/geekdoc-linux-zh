Network-connected computers already have a unique ID called the *Media Access Control* (*MAC*); one example is the ethernet ID. Your computer uses this ID to do network booting (diskless systems that only have RAM and all permanent storage is on a server). The ethernet ID is six bytes long, and you usually see it written in hexadecimal: 00:20:45:FE:A9:0B. Every ethernet card has one, and it is unique.

Unfortunately, you cannot use that ID for identifying your computer exclusively. It has two fundamental problems. First, every router server must acquire every ID on the network. The database of IDs could get very large and could significantly slow the routing time for each message. Second, not every interface has a MAC (PPP, for example).

The computer ID could have a built-in mechanism for routing the message. This mechanism is like addressing a letter: most general to most specific. Internet IDs solve the uniqueness issues while providing hints for the routing issues.

IP addresses provide several advantages over the hardware-supplied MAC. First the number can change (it is not fixed), so deploying consistent clusters of addresses is easier, and laptops don't run into problems. The network can map the IP to the hardware MAC using the *Address Resolution Protocol (ARP)*. See the Request For Comment #826 [RFC826] on the accompanying CD-ROM.

# Address Resolution Protocol (ARP)

The ARP is a simple translation table that takes the IP and fills in the associated MAC. All messages on the network must have a MAC so that the adaptor (or drivers) can pick up the message. The source may not know the MAC of the destination host, which hides deeply behind several routers. The router instead sends the message to routers that control the sub-networks (or subnets) defined in the IP address. When the message gets to a router with ARP, it checks the tables. If the router find the IP address, the packet's MAC gets the correct destination. Otherwise, the router sends a broadcast into the subnet to resolve the IP address.

# Internet ID Organization

The Internet ID uses a most-to-least-specific addressing scheme. Each ID is a four-byte number, like the ethernet ID. The first number, reading from left to right, is the network *class*. Look at Figure 2.1.

The IP address acts as a general roadmap to the routers. Each part of the address provides more specific information about where the destination is. Beginning with the network class, the address ends with the host number. You could easily compare it to an address on an envelope: The first line is the addressee, then the street address or box number. The detail decreases in the address until the state or country.

# 2
TCP/IP Network
LANGUAGE
FLUENCY