This means when a host needs to send something to another server across the Internet, it only needs to know how to get the packet to the router, and, therefore, only needs to know the MAC address of the router.

To see this happen on your network, do a tcpdump on your host and then visit a site that is elsewhere on the Internet, such as kernel.org. You will see an ARP request from your machine to your default route, a reply from your default route, and then the first packet from your host with the destination IP of the remote server.

# The ARP Header: ARP Works with Other Protocols, Too!

The ARP protocol is not specific to Ethernet and IP. To see why, let's take a quick peek at the ARP header (see Figure 11-8).

The first field that we see in the ARP header (which follows the Ethernet header) is the hardware type. The hardware type specifies the size of hardware address. Ethernet has the value of 1.

The next field is the protocol type. This specifies the protocol address mapping.

In case of IP, this size fields that immediately follow ARP the size of the addresses it is mapping. Ethernet has a size of 6, and IP has a size of 4.

The op field tells what needs to be done. ARP requests are 1, and ARP replies are 2.

Finally, there are the fields that we are trying to map. A request has the sender's Ethernet and IP addresses as the destination IP address filled in. The reply fills in the destination Ethernet address and responds to the sender.

> NOTE A variant of ARP, called RARP (which stands for Reverse ARP), has different values for the op field.

![](bbox=[0.14, 0.676, 0.857, 0.813])

| Ethernet Destination Address | Ethernet Source Address | Hardware Type | Protocol Type | op | Sender Ethernet Address | Sender IP Address | Target Ethernet Address | Target IP Address |
|---|---|---|---|---|---|---|---||
| 6 | 6 | 2 | 2 | 1 | 2 | 6 | 4 | 4 |