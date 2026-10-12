
## Glossary of Networking / Network Management Terms

Like many different technologies and industries, networking and network management have their own subculture and language. This glossary has been provided to bridge the gap and explain some of the more common terms used in this book and in the industry.

### Table C.1 Terms and definitions

| Term | Meaning |
| :--- | :--- |
| 100Base-TX | Known as Fast Ethernet, a 100 Mbps LAN technology based on the CSMA/CD network access method using two-pair Category 5 UTP cabling. Additional media types include 100Base-FX (fiber optic cable) and 100Base-T4 (four-pair Category 3 cabling UTP) |
| 10Base-T | A 10 Mbps LAN technology that uses the CSMA/CD network-access-method-based IEEE 802.3 specifications. Additional media types include 10Base2 (Thinnet, using thin coaxial cable), 10Base5 (ThickNet, using a large coaxial cable), and 10BaseFL (using fiber optic cable) |
| ACK | Acknowledgment; a response to a specific request. For instance, TCP provides acknowledgment for each packet transmitted |
| Agent | A software component found within networking devices or operating system processes that responds to queries from one or more network managers |
| arp | The UNIX command that displays or manipulates the ARP cache |
| ARP | Address Resolution Protocol; a network protocol that is responsible for mapping lower-layer network addresses (such as Ethernet) to higher-layer addresses (such as the Internet Protocol) |

### Table C.1 Terms and definitions (continued)

| Term | Definition |
| --- | --- |
| ARP cache | A list of ARP entries that consists of an IP address and datalink address used by a node on a TCP/IP network |
| ATM | Asynchronous Transfer Mode, a standard for cell relay that can be used to carry voice, data, and video in small 53-byte-size cells |
| Attachment Unit Interface | Known as AUI; defines the specification between an Ethernet media access unit (MAU) and DTE device; specifies how an Ethernet device connects to a transceiver used on a 10Base5 network |
| Backbone | A core LAN or WAN that uses one or more high-speed networking technologies with smaller networks branching off of them. LAN backbones connect different departments or groups of users. WAN backbone networks often provide connections to regional or remote locations |
| BER | Basic Encoding Rules. Standard method for encoding values of each ASN.1 type as a series of string octets or bytes |
| Bandwidth | Commonly used to describe the carrying capacity of a digital network facility that is typically measured in bits-per-second (bps). For example, 100Base-T Ethernet is said to have the capacity of 100 Mbps |
| BootP | Bootstrap Protocol based on the UDP network-layer protocol; provides a means to assign a host a dynamic IP address |

### Table C.1 Terms and definitions (continued)

| Term | Definition |
| :--- | :--- |
| Broadcast address | A special address used to simultaneously broadcast information to all stations on a network. Examples include IP broadcast (134.111.10.255) and Ethernet Broadcast (FF:FF:FF:FF:FF:FF) |
| Broadcast domain | A collection of network devices that share the same physical or logical network. Broadcast domains can be confined to a series of switched ports. When a broadcast occurs on this network, only those devices within the domain will receive it |
| Community string/community name | A string that provides password protection with SNMPv1 agents. If the SNMP manager has the community string, it is permitted to modify any object writable within the agent's MIB |
| CMIP | Common Management Information Protocol; an ISO standard for network management that provides some of the same functions as SNMP |
| Datalink Protocol | A low-level network protocol that functions on OSI model layer 2. It refers to the frame format and communications protocol. Popular datalink protocols include Ethernet, FDDI, and ATM |
| Enterprise MIB | A vendor-specific MIB that is defined under the enterprise branch and located under the iso.dod.internet.private branch. Many vendor MIBs such as Cisco and 3Com use this branch |

### Table C.1 Terms and definitions (continued)

| Term | Definition |
| --- | --- |
| Extensible agent | An SNMP agent that can be extended to include additional functionality by altering one or more configuration files or adding some custom functions |
| Get | An operation used to obtain the value of an MIB object from an SNMP agent. It serves as the primary way an SNMP manager retrieves MIB values |
| GetNext | Similar to the SNMP Get, this SNMP operation retrieves the "next" object in the MIB tree |
| Host resource MIB | The MIB that provides access to system-level objects such as memory usage, disk usage, running processes, etc. The UCD Agent provides access to these MIB objects |
| HPOV | Hewlett-Packard OpenView; one of the most popular network management packages |
| Internet Protocol | The Internet Protocol (IP) provides best-effort packet delivery and routing layer services. This protocol operates on layer 3 of the OSI model |
| Master agent | A central controlling agent that intercepts SNMP requests on the standard port and forwards these requests to one or more subagents. Usually, the sub-agents must be configured to function with the master agent |
| MIB | Management Information Base; defines objects contained within SNMP device agents that are used to manage the device |

### Table C.1 Terms and definitions (continued)

| Term | Definition |
| :--- | :--- |
| MIB-II | A standard MIB that provides access to a core set of objects defined in several groups. These include system interfaces, at, ip, icmp, tcp, udp, egp, and transmission |
| MIB browser | A user program that provides a hierarchical view of MIB objects for display or modification of individual object values |
| Multicast | An address that uses the class D range (224.0.0.0-240.0.0.0) for the destination IP address. Multicast represents a more effective mechanism than traditional unicast delivery for sending information to a large collection of devices |
| OSI | Open Systems Interconnection model. The model defines seven layers that are responsible for establishing connectivity between network devices |
| OUI | Organization Unique Identifier; part of the datalink address that represents the vendor of the equipment; used to identify datalink frames |
| Out-of-band management | Refers to the ability of a device to support remote management capabilities using a special interface that is not used for general connectivity |
| Packet | A generic term that describes the messages transmitted across a network. Packets contain a source, destination, and other associated information |
| PDU | Protocol Data Unit; the packet for SNMP message types. SNMP defines several PDU types: get-request, set-request, get-response, and trap |

### Table C.1 Terms and definitions (continued)

| Term | Definition |
| --- | --- |
| Probe | A device that attaches to a network that collects performance and packet information for later analysis and reporting. Probes usually implement RMON or some other network performance monitoring protocol |
| Polling | The act of retrieving specific information (MIB objects) from one or more agents. A manager is said to poll the agents for required information |
| RMON | Remote Monitoring Protocol. RMON is responsible for collecting network traffic and protocol information within a network probe. Many vendors have implemented RMON within their networking products |
| SAN | Storage Area Network. A network topology that integrates mass storage management hardware (i.e., disk farms) to computer systems using a standard-based networking infrastructure |
| Set | The operation used to change one or more MIB objects within an agent. An SNMP set operation requires security authentication to complete this task |
| SNMP | Simple Network Management Protocol. SNMP is the management protocol that provides management capabilities to individual systems and devices. SNMP defines a manager, agent, and MIBs |
| SNMPv1 | The first version of SNMP. This version included the core framework, SMIv1, and MIB-II definition |
