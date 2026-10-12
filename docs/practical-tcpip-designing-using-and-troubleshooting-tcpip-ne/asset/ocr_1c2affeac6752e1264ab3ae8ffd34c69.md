[In the case of FDDI (e.g., `fddi protocol arp`) and Token Ring (e.g., `tr protocol arp`), for most of those protocols, the protocol identification comes from the 802.2 Logical Link Control (LLC) header, which is usually layered on top of the FDDI or Token Ring header.

When filtering for most protocol identifiers on FDDI or Token Ring, tcpdump checks only the protocol ID field of an LLC header in so-called SNAP format with an Organizational Unit Identifier (OUI) of 0x000000, for encapsulated Ethernet; it doesn’t check whether the packet is in SNAP format with an OUI of 0x000000.

The exceptions are *iso*, for which it checks the DSAP (Destination Service Access Point) and SSAP (Source Service Access Point) fields of the LLC header, *stp* and *netbeui*, where it checks the DSAP of the LLC header, and *atalk*, where it checks for a SNAP-format packet with an OUI of 0x080007 and the AppleTalk etype.

In the case of Ethernet, tcpdump checks the Ethernet type field for most of those protocols; the exceptions are *iso*, *sap*, and *netbeui*, for which it checks for an 802.3 frame and then checks the LLC header as it does for FDDI and Token Ring, *atalk*, where it checks both for the AppleTalk etype in an Ethernet frame and for a SNAP-format packet as it does for FDDI and Token Ring, *aarp*, where it checks for the AppleTalk ARP etype in either an Ethernet frame or an 802.2 SNAP frame with an OUI of 0x000000, and *ipx*, where it checks for the IPX etype in an Ethernet frame, the IPX DSAP in the LLC header, the 802.3 with no LLC header encapsulation of IPX, and the IPX etype in a SNAP frame.]

+   1. `decnet src host`
+      True if the DECNET source address is *host*, which may be an address of the form `10.1.23`, or a DECNET host name. [DECNET host name support is only available on Ultrix systems that are configured to run DECNET.]

+   2. `decnet dst host`
+      True if the DECNET destination address is *host*.

+   3. `decnet host host`
+      True if either the DECNET source or destination address is *host*.

+   4. `ip, ipv6, arp, rarp, atalk, aarp, decnet, iso, stp, ipx, netbeui`
+      Abbreviations for:
+   
+      ```
+      ether proto p
+      ```
+   
+      where *p* is one of the above protocols.