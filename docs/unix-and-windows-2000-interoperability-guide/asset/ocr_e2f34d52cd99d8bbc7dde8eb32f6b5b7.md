# Chapter 4 • The Internet Layer

other. Similar applications on Windows NT and Windows 2000 can use NetBEUI, IPX/SPX, AppleTalk, and of course TCP/IP. All Windows network applications default to TCP/IP, and UNIX networking is practically synonymous with it.

In Chapter 3, "The Network Interface Layer," we looked briefly at the network interface layer, mentioning Ethernet and Fibre Channel in the major, and talked about that layer's drivers. Now we move up the "stack," if you will, to the major protocols that exist at or near the internet layer.

# 4.1 ARP

IP uses a 32-bit addressing scheme to send datagrams. However, these addresses are logical; in other words, they are not tied to a particular system. In fact, in Dynamic Host Configuration Protocol (DHCP) environments IP addresses for particular machines change all the time. (We will talk about DHCP later.) IP must respond on a protocol that sits between and the network interface layer to find the physical hardware address of a machine. That protocol is the Address Resolution Protocol, or ARP.

Let's assume your network is Ethernet. Ethernet sends frames to other systems using the 48-bit hardware address burned into the NIC (MAC address). When IP sends a datagram to Ethernet for delivery, that datagram contains the destination IP address. Since Ethernet does not understand IP addresses, it uses ARP to determine the appropriate hardware address of the machine owning the destination IP address, and once does so, delivers the frame. ARP then goes through the broadcast mechanism again. Cache entries for frequently destinations do not have to go through the broadcast last up to 10 minutes in Windows 2000, five minutes on HP-UX. Static entries do not expire.

ARP sends an ARP request in the form of a broadcast to find the hardware address of the destination system. All systems on the network hear this request, but only the owner of the destination IP address will respond with an ARP request containing its hardware address. If the IP address belongs to a system on a remote network, then the first-hop router will reply to the ARP request, though the ultimate destination may be several routers away. This service is known as proxy ARP.

# 4.1.1 Viewing the ARP Cache

4.1.1.1 Windows 2000

To view the ARP cache in Windows 2000, use the arp -a command. For example:

```
C:\>arp
```

Interface: 10.0.0.3 on Interface 0x2
Internet Address Physical Address Type
10.0.0.4 08-00-09-83-31-b1 dynamic
10.0.0.5 08-00-5a-d8-1e-a9 dynamic
10.10.1.1 00-60-b0-6a-8e-9c dynamic