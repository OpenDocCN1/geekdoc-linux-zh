In the main text we’ve implicitly assumed that the MAC address is hard-wired into the net-work interface card. While this is true, many cards allow the operating system to change the MAC address; fortunately, Windows and Linux systems don’t do this.

# IP using carrier pigeons

It has often been said that TCP/IP will run over wet string.

+   ☐ RFC-1149 1 April 1990 *IP Datagrams on Avian Carriers*

describes how TCP/IP can use carrier pigeons as transmission hardware. The Bergen Linux user group implemented this “standard” and a description of its work, with photographs and timings for *pings*, is at:

+   ☐ [http://www.blug.linux.no/rfc1149/](http://www.blug.linux.no/rfc1149/)

+   ☐ [http://www.blug.linux.no/rfc1149/pinglogg.txt](http://www.blug.linux.no/rfc1149/pinglogg.txt)

# ARP

We’ve described ARP only in the context of an Ethernet but it’s not limited to that – it works with token ring and other network types as well. ARP lets us use IP addresses exclusively and forget about MAC address, at a cost of a tiny amount of broadcasting. Perlman (Chapter 11) covers different ways of handling this issue. Or, you *could* design a network system that didn’t need ARP, by broadcasting every packet. This would work, but performance would be dreadful.

However, broadcasting has its uses. As we’ll see in Chapter 16, DHCP traffic between client and server *does* use broadcasts extensively; since a machine uses DHCP only at boot time, it imposes no significant load. Some other special-purpose networking applications use broadcasts exclusively: one example we’ve seen is a “find-my-device” application for a hardware firewall appliance. If we receive a firewall back from a customer without knowing what the IP address is, we can run this program. It broadcasts a special packet using a proprietary protocol. The firewall hears this and broadcasts a reply. This communication works no matter what the IP address and netmask setting are on our PC or on the appliance – perfect for a diagnostic tool, and negligible performance impact as only two packets are exchanged in total.

As an interesting aside on how `tcpdump` can give you insights into your network, if you run it as `tcpdump -n -e arp` for a few days, you can process the output (e.g. with a Perl script) and automatically construct a list of (IP number, MAC address) mappings. We keep a recent copy of this list on the wall above our desk.

ARP has a variant called “proxy ARP” where one device sends the ARP reply on behalf of another. This is useful in firewalling (Chapter 24) and dial-up networking (Chapter 26) where we’ll explain it further. For RARP (“reverse ARP”), formerly used for automatically assigning an IP address to a diskless workstation, see the Notes in Chapter 16.

For more on ARP, see Stevens, Chapter 4.