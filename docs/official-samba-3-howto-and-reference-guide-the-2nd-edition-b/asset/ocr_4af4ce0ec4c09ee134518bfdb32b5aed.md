Network packets that are sent over the physical network transport layer communicate not via IP addresses but rather using the Media Access Control address, or MAC address. IP addresses are currently 32 bits in length and are typically presented as four decimal numbers that are separated by a dot (or period) — for example, 168.192.1.1.

MAC addresses use 48 bits (or 6 bytes) and are typically represented as two-digit hexadecimal numbers separated by colons: 40:8e:0a:12:34:56.

Every network interface must have a MAC address. Associated with a MAC address may be one or more IP addresses. There is no relationship between an IP address and a MAC address; all such assignments are arbitrary or discretionary in nature. At the most basic level, all network communications take place using MAC addressing. Since MAC addresses must be globally unique and generally remain fixed for any particular interface, the assignment of an IP address makes sense from a network management perspective. More than one IP address can be assigned per MAC address. One address must be the primary IP address; this is the address that will be returned in the Address Resolution Protocol (ARP) reply.

When a user or a process wants to communicate with another machine, the protocol implementation ensures that the “machine name” or “host name” is resolved to an IP address in a manner that is controlled by the TCP/IP configuration control files. The file `/etc/hosts` is one such file.

When the IP address of the destination interface has been determined, a protocol called ARP/RARP is used to identify the MAC address of the target interface. ARP is a broadcast-oriented method that uses User Datagram Protocol (UDP) to send a request to all interfaces on the local network segment, using the all 1 MAC address. Network interfaces are programmed to respond to two MAC addresses only; their own unique address and the address ff:ff:ff:ff:ff:ff. The reply packet from an ARP request will contain the MAC address and the primary IP address for each interface.

The `/etc/hosts` file is foundational to all UNIX/Linux TCP/IP installations and as a minimum will contain the localhost and local network interface IP addresses and the primary names by which they are known within the local machine. This file helps to prime the pump so a basic level of name resolution can exist before any other method of name resolution becomes available.

# 28.3.2  `/etc/resolv.conf`

This file tells the name resolution libraries:

+   - The name of the domain to which the machine belongs.

+   - The name(s) of any domains that should be automatically searched when trying to resolve unqualified host names to their IP address.

+   - The name or IP address of available domain name servers that may be asked to perform name-to-address translation lookups.