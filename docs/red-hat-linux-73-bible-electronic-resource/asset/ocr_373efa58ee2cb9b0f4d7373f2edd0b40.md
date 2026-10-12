# 604 Part IV: Red Hat Linux Network and Server Setup

> **TIP:** If you are looking to upgrade your network in the near future, but still have a lot of computers around that run at 10 Mbps, you may want to consider buying new NICs that run at both 10 Mbps and 100 Mbps. When you switch over to 100 Mbps, you will have fewer cards to replace.

• **Cables** — Star and bus topologies require different cabling. Wireless LANs, as you might guess, require no cables, but may require additional antennas depending on the distances and obstacles (see the section “Setting Up a Wireless LAN” for details).

For star topologies, cables are referred to as *twisted-pair*. Category 5 wiring, which contains four twisted-pair sets per wire, is the most common type of wiring used for LANs today. A connector at each end of the cable is an RJ-45 plug, similar to those used on telephone cables. Ethernet interfaces are either 10Base-T (10 Mbps speeds) or 100Base-TX (100 Mbps speeds). These cables plug into the computer’s NIC at one end and the hub at the other.

For bus topologies, coaxial cables are used. These cables are also referred to as thin Ethernet cables, or *thin net*. (There are also thick net cables, which are more expensive and more cumbersome to deal with. These are rarely used and are primarily for network backbones.)

The connector on coaxial cables is a barrel connector (BNC). A “T” connector attaches to the BNC port on the NIC. In the middle of the daisy chain, each computer connects to two adjacent computers using the T connector. At the two ends of the chain, the computer connects to one adjacent computer, then uses a terminator at the other end of the T to end the chain.

Figure 15-5 shows an example of a twisted-pair cable with an RJ-45 connector used for star topologies. Figure 15-6 shows a coaxial (thin net) cable with a BNC connector and a T connector used for bus topologies. A terminator at the end of the T connector shows that this is the end of a chain. If it were in the middle of the chain, the other side of the T would be connected to the next computer in the chain.

![](bbox=[0.05, 0.64, 0.45, 0.87])

Figure 15-5: A star topology’s twisted-pair cables have RJ-45 connectors (similar to telephone-cable connectors).