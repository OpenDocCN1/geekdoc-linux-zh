
cache. If it does, the existing binding is used; otherwise the ARP request is sent. As a result of the cache, network traffic is reduced because ARP requests are only made when devices are not known. Also, application performance is improved because the sender's ARP request can be satisfied by using the cache instead of transmitting a packet on the network. Finally, the cache provides the administrator with a way to view connectivity between the higher-level protocols and the network hardware. As we will see later in this book, inspecting the ARP cache can be a powerful way to troubleshoot network and system problems.

Here is one interesting question regarding the ARP cache: When should the bindings be discarded from the cache? The answer is not simple. If we presume to keep the ARP cache populated with entries forever (or until the system is restarted), the possibility exists that the cache will contain invalid information. Consider, for example, a network that contains systems *monet* and *rembrandt*, which are in the midst of communicating when the network interface card (NIC) fails on *rembrandt* and is subsequently replaced. The new NIC will contain a new *data link* address unless the administrator has *changed* it after the interface was installed. As a result, *monet* can't talk to *rembrandt* any longer because the cache on *monet* contains an invalid *data link* address for *rembrandt*. On the other hand, we can take the approach that bindings in the ARP cache should expire in a relatively short period of time, say every 30 seconds. Unfortunately, this will adversely affect network performance because more network broadcasts will be needed because the ARP cache will be very small. However, it will address the problem of the incorrect bindings for NIC that have recently been replaced because the old entry would have been purged in a reasonable period of time after the new NIC was operational.

Perhaps the best solution to this problem can be described by *taking the middle of the road* approach. That is to say, the binding expiration shouldn't be too small to be ineffective but also not too long to address changes in the network. In general, most UNIX systems will delete ARP entries in approximately 20 minutes. Some versions of UNIX also permit the administrators to change the ARP cache timeout to suit their:
- Datalink Address Format
- individual network requirements and, when necessary, alter it to address other network-related problems

### Datalink Address Format

As indicated, datalink addresses are expressed in 48 bits (six bytes) and separated by colons. This colon notation is used as the primary method to represent these hardware addresses. Some UNIX network management tools, such as the ifconfig and arp commands, use this format. Datalink protocol addresses for FDDI, Ethernet, and TokenRing contain a vendor code identification number and serial number. This information can be used in node identification for inventory purposes. The IEEE registry authority assigns the vendor portion to those organizations that produce network hardware and have requested a vendor code. These codes are also referred to as Organization Unique Identifiers (OUI). The first three bytes of the address represent the manufacturer or vendor of the device, and the remaining three bytes represent the serial number of the unit, as depicted in Figure 3.22.

![](img/f265c9d1f2610aca197c430cbfcd51f5_131_0.png)

Figure 3.22 Datalink address format.

Often on a multi-homed system, the datalink addresses will be shared among all the defined interfaces. This may even be true for systems that contain different network interface types (i.e., Ethernet and FDDI). Table 3.7 shows some of the most common vendor codes. Notice that more than one vendor code might be associated with the same vendor. This may be true, for example, when one company purchases another company and their products. In this case, the vendor code of the company that was purchased now falls under the other company. This is why Table 3.7 contains multiple entries for both 3Com and Cisco. Knowing a few of these addresses can be very handy during network debugging to help identify the type of device and vendor to which a particular packet belongs. If you are interested in finding a vendor not listed in the Table 3.7, access the IEEE Web site at http://standards.ieee.org/regauth/oui/oui.txt.

### Table 3.7 Sample vendor OUI codes

| **Vendor Code** | **Vendor** |
|---|---|
| 00:20:AF<br>00-80-3E<br>00-C0-D4<br>(many more) | 3Com Corporation<br>Formerly Synernetics, Inc.<br>Formerly AXON, Inc. |
| 08-00-2B<br>AA-00-00<br>AA-00-03<br>AA-00-04 | Formerly Digital Equipment Corporation (DEC), now owned by Cabletron Systems |
| 00:00:0C<br>00-E0-B0<br>00-E0-F7<br>00-E0-F9<br>00-E0-FE<br>00-06-7C<br>00-06-C1<br>00-10-07<br>(many more) | Cisco Systems, Inc.<br>(Includes a large list of former companies) |
| 00-60-69 | Brocade Corporation |
| 00-00-81<br>00-00-A2<br>00-80-E3 | Formerly Bay Network, Inc.<br>Formerly Coral Networks |
| 00-E0-81 | Packet Engines, Inc. |
| 08:00:5A | IBM Corporation |
| 08:00:20 | Sun Microsystems, Inc. |
| 08-00-09 | HP Corporation |
| 00-10-E3 | Compaq Corporation |

102

Chapter 03 / TCP/IP Protocol Suite

Accessing this Universal Resource Locator (URL) will display the entire OUI file. Please note: This file is quite large (over 900K) and is growing! If you're not interested in seeing the entire contents of the OUI file, then search for the specific vendor codes you are looking for by accessing `http://standards.ieee.org/regauth/oui/index.html`.

Accessing this URL will display the page shown in Figure 3.23.

![](img/f265c9d1f2610aca197c430cbfcd51f5_133_0.png)

Figure 3.23 IEEE OUI search page.

Should you wish to search for a vendor, enter the name of the company in the search text box field. Also, if you know the OUI, but want the vendor, enter the address instead. Next, click the *Search!* button. Figure 3.24 shows the result obtained when the Brocade company was searched.

![](img/f265c9d1f2610aca197c430cbfcd51f5_134_0.png)

Figure 3.24 OUI search results.

## Core System Utilities and Tools

This chapter provides a detailed overview of the commands and utilities that are available with the Linux operating system. Many of the tools discussed are part of a common set of tools and available on many other different UNIX platforms. For instance, the arp command operates in a similar fashion and has many of the same command-line options across Solaris, HPUX, and AIX systems.

The software discussed in this section includes tools that can assist the network manager or administrator in handling network-related tasks and address specific network problems. This chapter covers the following tools:

| Command | Page |
| --- | --- |
| arp | 106 |
| ifconfig | 115 |
| netstat | 125 |
| ping | 143 |
| tcpdump | 153 |
| traceroute | 171 |

### ARP Tool

#### General Description

The `arp` command displays and manipulates the network address table on a local UNIX system. The address resolution protocol table, also known as the **ARP cache**, contains a complete list of all datalink protocol to IP address mappings for the local network. Recall from Chapter 3 that the ARP protocol is a dynamic facility that maps datalink addresses such as Ethernet to IP addresses. Whenever a system wants to transmit a message, it must first know the low-level (i.e., datalink) address for the target system. Many networking tools, such as `telnet`, `ftp`, and others, indirectly use the ARP table.

The `arp` command provides the ability to view and modify the ARP table. Note that the terms ARP table and ARP cache can be used interchangeably and reference the same thing. Also, the terms **binding** and *mapping* refer to an ARP entry as well. Regular UNIX (non-root) users may display the ARP cache but cannot make any changes. The reason for this should be obvious; users could make alterations to the cache that would affect connectivity for all users.
