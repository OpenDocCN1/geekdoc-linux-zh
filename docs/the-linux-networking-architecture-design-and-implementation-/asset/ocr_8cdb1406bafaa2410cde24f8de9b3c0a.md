# B.3 Information in the /proc Directory

ksym shows the symbols exported by the kernel and their memory addresses in the kernel. This table is important for supporting kernel modules. (See Section 2.4.) dma lists the occupied DMA channels and I/O ports, plus the instances that reserved them.

slabinfo This file holds information about memory caches used in the kernel. (See Section 2.6.2.) Of interest for the network part are mainly skb_head_cache and the caches for the TCP transport protocol. To display information about a cache, you have to write a corresponding entry in the file /slab.c.

Entries in the /proc/net Directory The entries in /proc/net directory are listed below. Some of these entries are only visible if the appropriate functionality was embedded in the kernel (e.g., IP Chains). In addition, there is a separate version for the new Internet Protocol Version 6 for many entries that refer to the Internet Protocol 4. These entries can be identified by a 6 at the end, e.g., raw6 or igmp6.

+   arp outputs the content of the kernel ARP table. (See Chapter 15.)ndev shows registered network devices and their statistical data.
d_mcast lists those layer-2 multicast groups to which a network device listens (index, device name, number of references, number of bound addresses).
igmp lists those IP multicast groups to which the computer is subscribed. (See Chapter 17.)
ip_fwchains contains rules for IP Chains. (See Chapter 19.)
ip_fwnames holds firewall lists.
ip_mask holds the masquerading tables.
ip_masquerade holds the main masquerading table.
ip_mr_vifs lists the virtual network devices for multicast (VIF).
ip_mr_cache holds the multicast routing cache. (See Chapter 17.)
etstat show detailed network statistics (for SNMP purposes).
row shows statistics for Raw sockets.
route shows the kernel routing table.
rpc is the directory with RPC information.
t_cache holds routing cache information. (See Chapter 16.)
smp holds the Management Information Base (MIB)—data for SNMP.
socket holds socket statistics.
tcp holds information about TCP sockets.
t_rif shows the token RIF routing table.
udp holds information about UDP sockets.
unix holds information about UNIX domain sockets.
wireless holds information about wireless LANs (e.g., IEEE 802.11).
psched holds parameters for the packet scheduler.
netlink is a list of PF_NETLINK sockets.