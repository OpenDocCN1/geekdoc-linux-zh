| Device Type | TCP/IP Protocols |
| --- | --- |
| 3Com CoreBuilder switch | HTTP, FTP, Telnet, and SNMP |
| 3Com RMON probe | TFTP and SNMP |
| Cisco 7000 router | HTTP, FTP, Telnet, and SNMP |
| Brocade fibre channel switch | HTTP, Telnet, and SNMP |
| Lexmark laser printer | FTP and SNMP |

TCP/IP is independent of the datalink protocol and can be used with many different networking technologies, including FDDI, Ethernet, ATM, TokenRing, Frame Relay, and SMDS. TCP/IP makes it possible to build a truly heterogeneous network consisting of products and network technologies from many different vendors and sources. In fact, the Internet, which is considered the world's largest network, consists of devices from many networking vendors that operate together. That's not to say the Internet doesn't have its share of networking issues or problems, but, for the most part, many would agree that interoperability between equipment vendors isn't a major factor for the established core set of TCP/IP protocols.

From a management standpoint, many of the tools used to administer TCP/IP systems are consistent across most UNIX operating system versions. These tools are described in Chapter 6, “Network Management Agents.” However, one issue that can be a problem is that each UNIX operating system vendor can and does implement non-protocol details differently. For example, how the IP address information is stored on each network device is not covered by any RFC standard, nor should it be. The present TCP/IP suite provides a mechanism to dynamically assign IP addresses to devices, and it also mandates that they be uniquely assigned to each device attached to the network. However, IP addresses are stored on a local system and are not a protocol matter, but rather a network management or system configuration issue, which is traditionally resolved at the operating system level. Each operating