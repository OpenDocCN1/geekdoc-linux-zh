With these fields and the packet ID, the IP subsystem can fragment and reassemble your packet. If the subsystem cannot get all the pieces within a specified time, it drops the packet and sends an error back to the originator.

# time_to_live (TTL) Field

This field originally counted the number of seconds a packet could survive on the network during transit. Later, the meaning changed to the number of router hops. A hop is the transition through a host or router (node) where the node actively moves a packet from one network to another.

This 8-bit field permits up to 255 router hops before being discarded. When a router or forwarding host gets the packet, it decrements this field by one. If the field equals zero before arriving at the destination, the node drops the packet and sends an error to the source. The TTL field keeps the network from bouncing a packet around indefinitely.

Use the IP_TTL socket option to set this value (see Chapter 9). Alternatively, you can set it directly if you elect direct IP header manipulation (IP_HDRINCL).

# protocol Field

Every packet on the Internet has an assigned protocol value, and ICMP (IPPROTO_ICMP or 1), UDP (IPPROTO_UDP or 17), and TCP (IPPROTO_TCP or 6) each own a code. The protocol tells the system how to treat the incoming packet. You can set this value with the SOCK_RAW option in the socket() system call. The protocol value is the last parameter of the call. The kernel's netinet/in.h header file lists many more. (Remember that even though the kernel includes a protocol definition, it might not support it.)

# options Field

The IP subsystem can pass several options with each packet. These options include routing information, timestamps, security measures, routing record, and route alerts. This field can be up to 40 bytes long. Because some of the options are system dependent, you are unlikely to ever touch these options directly.

# data Field

Your message goes here and can include up to 65,535 bytes (minus 60 bytes, the maximum size of the header). The data section includes any header information that the higher protocols need. For example, ICMP requires 4 bytes, UDP requires 8 bytes, and TCP requires 20–60 bytes.

The Internet packet system bases all its IPv4 packets on this structure. Each layer on top of this adds features and reliability.

![](bbox=[0.83, 0.45, 0.99, 0.61])