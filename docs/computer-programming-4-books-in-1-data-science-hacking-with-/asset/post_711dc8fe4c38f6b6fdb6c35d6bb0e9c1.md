
## Understanding Ethernet

Ethernet network architecture is the most widespread of all network architecture all over the globe. We're going to examine the depths of this architecture and most likely find out why this architecture is as popular as it is.

Most network peripheral components have a built-in NIC. As a result, they can be easily plugged into an Ethernet wall outlet. It must be noted that the standard predetermined Ethernet length of wire of 100m from a hub or switch remains so even when it comes to NIC-equipped print servers and printers; just as it is the case with workstations.

Printers that do not have a built-in NIC can still be used on a network by getting a connection with a network print server through a parallel, serial or USB port, or onboard NIC.

### Ethernet Network Access Strategy

Suffice to say, Ethernet is a passive network architecture that embraces the wait-and-listen approach. It is also referred to as contention-based architecture since all computers on the network have to contend with the time of transmission on a given network medium.

Access to Ethernet networks is via CSMA/CD. This simply means that the network hosts have to listen to the network until the transmission medium is clear so that they can also transmit. Basically, they have to “sense” and determine that the line is indeed clear to initiate their own data transmission processes. A network host only sends out its data once it “feels” that the transmission is clear. In case there are multiple transmissions, a collision or collisions take place on the transmission medium. The machines sense the collisions and immediately halt their transmission processes.

One of the machines starts the retransmission as the others wait for the line to clear before they can retransmit their data. This process happens until all the network have completed their transmissions.

In a similar fashion, hosts wait and listen on the line for data meant for them. When a particular host senses that incoming is mean for them, they open door for its reception and actually does receive the data onto its NIC interface. Ethernet is characterized by frequent collisions. As a result, some devices have collision [counters] to prompt you when a collision happens. In fact, collisions are the main limitations of the Ethernet architecture. On the other hand, Ethernet is the most affordable of all other network architectures.

**Note:**

- Collisions slow down the network.
- Excess collisions may bring down a network completely.

### Fast Ethernet

The traditional Ethernet has a speed of 10Mbps. Fast Ethernet offers a speed that is higher than the original 10Mbps. It has a 100Mbps transfer rate. The throughput is higher than the traditional Ethernet standard since the time it takes to transmit data over a network medium has been minimized by [a] whopping factor of 10. Thus, Fast Ethernet works at a rate that is 10 times the traditional speed of 10Mbps. Traditionally, hubs and other connecting devices were designed to accommodate the 10 Mbps transfer rate. For such devices, Fast Ethernet is not supported. Fortunately, many connecting devices are being [equipped] with NICs that can comfortably handle both 10Mbps and 100Mbps transfer rates. That means that the devices can accommodate both the original 10Mbps Ethernet as well [as] the Fast Ethernet.

### Gigabit Ethernet

This is another version of Ethernet that is even faster than Fast Ethernet. It uses the same data formats and IEEE Ethernet specifications just like the other Ethernets—10Mbps and Fast Ethernet. With Gigabit Ethernet, users are able to enjoy 1000Mbps transfer on a network. Unlike Fast Ethernet that operates on both twisted-pair cables and fiber-optic cables, Gigabit Ethernet was initially restricted to fiber-optic cabling. This required that a LAN be set up with specialized servers and high-speed switches. Gigabit Ethernet was considered to be a backbone for large LANs that required high transmission speeds. Currently, anyone can practically enjoy the amazing high speeds of Gigabit Ethernet since it is being bundled out in network cards that can be conveniently installed in network servers and network clients.

### Ethernet IEEE Cable Specifications

The following is a list showing some of the Ethernet specifications:

- 802.3 for Ethernet LAN
- 802.5 for Token-Ring LAN
- 802.7 for Broadband TAG
- 802.8 for Fiber-Optic TAG
- 802.9 for Data Networks and Integrated Voice
- 802.10 for Network Security
- 802.11 for Wireless Networks

Note: TAG stands for Technical Advisory Group

The following points must be taken into account:

- Ethernet is well-defined by the IEEE specifications of 802.3.
- It works at the Data Link layer of the OSI model.
- A number of the various IEEE types of Ethernet are available depending on the nature of cabling preferred on the given computer network.

These types of Ethernet—Gigabit Ethernet and Fast Ethernet—are designated by 3-part names, like **10BASE-T**. The first section of the name describes the transmission speed. For instance, 10 specifies 10Mbps Ethernet.

The second part of the name, which is "base" for all the different forms of Ethernet, indicates that the Ethernet signal is *baseband*. This means that the data drifts in a stream as one signal. This type of data transmission cannot allow the transmission of multiple channels of data or information as can the alternative—the *broadband*.

The last part of the Ethernet type name specifies the type of cable in use. For instance, in 10BASE-T, the *T* indicates a twisted-pair cable, and it is presumed to be unshielded twisted-pair cable.

**10BASE-T**: This type of Ethernet works with a twisted-pair cable (unshielded twisted cable). The maximum cable length (without signal amplification) is 100m. 10BASE-T is operable on a star topology.

**10BASE-2**: This type of Ethernet works with a fairly flexible coaxial cable (RG-58A/U) or a *thinet*, with a maximum cable length of 185m (this is rounded off to 200. Thus, the 2 in 10BASE-2). With the use of T-connectors to link the cabling to the network hosts' network cards, 10BASE-2 uses a bus topology. Though 10BASE-2 has always been the most pocket-friendly option for the Ethernet implementation, 10BASE-T setups are presently the most widespread.

**10BASE-5**: This is [a] type of Ethernet that uses a large-gauge coaxial cable (also referred to as *thicknet*), and the hosts on the network are linked to a main trunk line. The cables from the network hosts join the main trunk cable using vampire tabs, which pierce the primary trunk cable.

**100BASE-TX**: This is the type of Fast Ethernet that relies on the same Category 5 UTP cabling that is available on 10BASE-T Ethernet. This [standard] can also employ 100-Ohm shielded twisted pair cable. The maximum cable length in the absence of a repeater is 100 meters.

**100BASE-T4**: This is the sort of Fast Ethernet that runs over Category 5 cabling, as can the 100BASE-TX. However, it can as well run over lower-grade twisted-pair cabling like Categories 3 and 4. In this type of Ethernet, the maximum cable run is the standard 100m length.

**100BASE-FX**: This is the sort of Fast Ethernet that spans over fiber-optic cable with a maximum length of 412m.

**1000BASE-T**: This is the kind of Gigabit Ethernet that delivers 1000Mbps over Category 5 twisted pair cables.

**10 Gigabit Ethernet**: This is the kind of Ethernet that delivers 10 billion bits per second over fiber optic cables.

## Peer-to-Peer Communication

The peer-to-peer network setup offers a simple and cost-friendly networking solution in which the basic networking functions are needed. Peer-to-peer is ideal where file sharing and other basic resources such as printers [are shared]. In this networking arrangement, there is no need for a dedicated server. The elimination of a network [server] from the budget makes this kind of networking a highly pocket-friendly venture. It must be understood that network servers are quite expensive. They significantly contribute to the overall cost of a network. Therefore, its omission from the shopping list is a great way of cutting down on the installation cost of a network, as well as overall management of the network. It is the most ideal option for the implementation of small networks.

### Features of Peer-to-Peer Networking

The following are the main features of Peer-to-Peer Networking:

- All network computers have equal privileges. They behave like peers.
- Each network host acts like both client and server. Essentially, a network host can send out requests to another network hosts. Similarly, each host can receive requests from other [hosts] on the network.
- There is [no] centralized administration of resources. This is due to the omission of a dedicated server from the setup. This also forms a concrete basis for connoting a peer-to-peer network as a workgroup. The peers collaborate freely without any centralized control or regulation.
- You only need to install an operating system on each peer and then physically connecting the peers via the NICs (NICs are not even necessary when working with Macintosh computers).

### Merits of Peer-to-Peer Communication

The following are the main advantages of a peer-to-peer network implementation:

- Peer-to-peer network implementations are easy [to] install since they only involve the installation of operating systems on peer computers and physically connecting them.
- They are less expensive since a costly server computer is not needed. Furthermore, a Network Operating System (NOS) is also not needed.
- All [tools] required are readily available, most of which comes packaged in your operating system.
- The network implementation is reliable since failure or malfunction of a single peer does not lead to failure of another, or failure of the entire network.

### Demerits of Peer-to-Peer Communication

The following are the main limitations of a peer-to-peer network:
