the anycast address, was defined, which allows you to send a packet to an arbi-trary node from within a group.

Simplified header format: Some of the IPv4 packet-header fields are no longer sup-ported, or are now optional, to reduce the cost involved in processing IPv6 packets.
Extension headers: The way IPv6 encodes information is completely different from that of IPv4, enabling more efficient forwarding, less strict limitations with-ngard to the length of options, and more flexibility for new, future packet options.
Flow labeling: IPv6 is able to mark packets that belong to a specific stream. This allows the sender to request special handling of these packets. enabling a much-better support of service qualities, such as priority handling or real-time services.
Authentication and data protection: IPv6 specifies extensions to support authenti-cation, integrity, and confidentiality of data.

# 23.2.1 Addressing

The address space, extended from $2^{32}$ (IPv4 to $2^{128}$ (IPv6) addresses, requires a new address notation. The preferred and abbreviated notation is the hexadecimal (e.g., FEDC:BA98:7654:3210:FEDC:BA98:7654:3120). Each group (i.e., one block between two columns, or between the beginning/end and a colon) represents 16 bits. Leading zeros can be omitted, so one group can consist of four hex-adecimal numbers. In addition, it is assumed that many consecutive blocks consist of zeros, as a compressed notation was introduced: Each address may contain at most one occur-rence of two colons. In between, as many zeros are necessary as to reach the full length of an address. The following examples show this notation (the meaning of each address will be discussed further below):

A "loopback"::

::1 or 0:0:0:0:0:0:0:1 = 00000000:00000000:00000000:00000001

A normal address:

= F835::12 or F835:0:0:0:0:0:12
= 0F83:0005:0000:0000:0000:0000:0012

Alternatively, addresses can be represented in mixed form, composed of the new hexadecimal notation and the decimal IPv4 notation. The format is then-x:x:x:x:x:x:x:d.d.d, where x represents the hexadecimal groups of IPv6 and d stands for the decimal IPv4 count. One example would be 0:0:0:0:0:0:0:ffff:129.13.64.5 (or ::ffff:129.13.64.5 in the abbreviated form). This approach becomes useful if you are thinking of embedding IPv4 protocols in IPv6.

As IPv4, IPv6 supports unicast and multicast addresses. A new form of communication introduced in IPv6 is anycast. Anycast is a mixture of unicast and multicast: A packet is sent to one computer in a multicast group, where the network decides which computer this is. The "broadcast" address of IPv4 (255.255.255.255) does not exist in IPv6. This functionality, which was mainly used by ARP (Address Resolution Protocol) to resolve it is achieved by the use of multicast addresses in