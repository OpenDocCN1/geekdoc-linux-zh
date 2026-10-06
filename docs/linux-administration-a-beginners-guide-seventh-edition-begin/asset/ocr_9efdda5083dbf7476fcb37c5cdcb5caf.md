# CHAPTER 10 Knobs and Dials: API (Virtual) File Systems 273

| Filename | Contents |
| /proc/version | Current version number of the kernel, the machine on which it was compiled, and the date and time of compilation. |
| /proc/scsi/* | Information about all of the SCSI devices. |
| /proc/net/arp | Address Resolution Protocol (ARP) table (same as output from arp -a). |
| /proc/net/dev | Information about each network device (packet counts, error counts, and so on). |
| /proc/net/snmp | Simple Network Management Protocol (SNMP) statistics about each protocol. |
| /proc/net/sockstat | Statistics on network utilization utilization. |
| /proc/sys/fs/* | Settings for file system utilization by the kernel. Many of these are writable values; be careful about changing them unless you are sure of the repercussions of doing so. |
| /proc/sys/net/core/netdev_max_backlog | When the kernel receives packets from the network faster than it can process them, it places them on a special queue. By default, a maximum of 1000 packets is allowed on the queue. Under extraordinary circumstances, you may need to edit this file and change the value for the allowed maximum. |
| /proc/sys/net/ipv4/icmp_echo_ignore_all | Default = 0, meaning that the kernel will respond to Internet Control Message Protocol (ICMP) echo-reply messages. Set this to 1 to tell the kernel to stop replying to these messages. |
| /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts | Default = 1, meaning that the kernel will not allow ICMP responses to broadcast or multicast addresses. |
| /proc/sys/net/ipv4/ip_forward | Default = 0, meaning that the kernel will not forward packets between network interfaces. To allow forwarding (as for routing), change this to 1. |
| /proc/sys/net/ipv4/ip_local_port_range | Range of ports Linux uses when originating a connection default = 32768–61000. |
| /proc/sys/net/ipv4/tcp_syncookies | Default = 1 (On). Change to 0 (Off) to disable protection for the system against SYN flood attacks.

# Table 10-1 Useful Entries Under /proc (Continued)