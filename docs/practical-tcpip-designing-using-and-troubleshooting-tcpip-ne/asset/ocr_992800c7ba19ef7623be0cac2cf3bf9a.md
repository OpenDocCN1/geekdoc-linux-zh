The introduction to RFC-1519 is very readable, describing how rapidly the use of IP addresses is growing, the problems of running out of IP addresses, and how CIDR helps. (We'll also see in Module 23.2 how network address translation (NAT) lets you connect a very large LAN to the Internet using only a handful of IP addresses. That has gone a long way to eke out the limited set of IP addresses that are available.)

# Special addresses

The standard private addresses for use on test networks, VPNs, etc. are defined in

+   ☐ RFC-1918 **February 1996** *Address Allocation for Private Internets*

(10.0.0.0 was the address of the old ARPANET, which was the precursor of the Internet as we know it.)

Packets addressed to private addresses ought to be blocked by your Internet router as they leave your site. However, if your ISP hasn't set things up correctly, they may travel some distance before being dropped. You can see this by doing a **traceroute**, e.g. “traceroute 10.4.5.6.” Packets with addresses that ought never to appear on this network, but that have arrived here because of bad routing entries (e.g. 10.*.*.* packets travelling over the Internet backbone) are often called “Martians.”

Private addresses were first suggested in:

+   ☐ RFC-1597 **March 1994** *Address Allocation for Private Internets*

which gives other examples of where you might want non-routable, private addresses: information displays at an airport, or cash registers in a retail chain, adding that these would probably never need Internet connectivity. Opinions are changing: a big benefit of *IP version 6* (or Ipng – IP Next Generation – Web Appendix 4) is that its huge address space allows *every* TCP/IP device to have a unique IP address and so be Internet accessible if required. You could use your TCP/IP mobile phone to tell your TCP/IP microwave oven to start cooking, and to turn on your TCP/IP central heating boiler as you travel home from work. With this world view, you can easily imagine that an airline would update its information display in Singapore from its HQ in Dublin, or a retailer in Arkansas might update its cash registers in London stores with details of global special deals. Having every device potentially Internet-connected may be desirable, at least in principle. (On the other hand, this level of accessibility poses horrific security problems.)

The 192.0.2.* addresses used in documentation ought not to be routed either, but as this usage isn't an official standard, they may be. See:

+   ☐ http://www.isi.edu/~bnanning/dsua.html

(or if that isn't available, search for “draft-manning-dsua” using Google or similar. IP numbers for small self-configured networks should never be routed. See

+   ☐ MS-KB-Q220874 *Automatic Windows 98/Me TCP/IP Addressing Without a DHCP Server*

which describes “Automatic Private IP Addressing” (APIPA).