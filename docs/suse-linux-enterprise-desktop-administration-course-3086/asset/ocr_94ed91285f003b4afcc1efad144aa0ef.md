# Internet Layer

The Internet layer of the TCP/IP model ensures the connection between individual hosts in the network beyond the limits of individual networks in the Internet, as shown in Figure B-13.

![](bbox=[0.1, 0.22, 0.78, 0.55])

Figure B-13

The main tasks of the Internet layer are providing an address space for the Internet, routing, and data transfer between end systems (host computers).

The following protocols are used by the Internet layer (with IP as the most popular):

+   - Address Resolution Protocol (ARP)
+   - Internet Protocol (IP)
+   - Internet Control Message Protocol (ICMP)

# Address Resolution Protocol (ARP)

ARP (Address Resolution Protocol) (RFC 826) resolves IP addresses to hardware addresses (MAC addresses, Media Access Control).

The MAC address is always composed of six bytes (in hexadecimal notation). The first three bytes indicate the manufacturer, and the last three bytes are the serial number of the network card.

If two network cards are present, both with the same serial number, you can specify (under Linux) which MAC address the network card should use to reply.