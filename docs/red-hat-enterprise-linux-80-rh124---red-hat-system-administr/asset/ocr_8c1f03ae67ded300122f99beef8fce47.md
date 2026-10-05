# CHAPTER 1 | Managing networking

New versions of Red Hat Enterprise Linux use a different naming system. Instead of being based on detection order, the names of network interfaces are assigned based on information from the firmware, the PCI topology, and type of network device.

Network interfaces start with the type of interface:

+   - Ethernet interfaces begin with en
- WLAN interfaces begin with wl
- WWAN interfaces begin with ww

The rest of the interface name after the type will be based on information provided by the server's firmware or determined by the location of the device in the PCI topology.

+   - on indicates that this is an on-board device and the server's provided index number N for the device. So en01 is on-board Ethernet device 1. Many servers will not provide this information.
- sn indicates that this device is in PCI hotplug slot N. So ens3 is an Ethernet card in PCI hotplug slot 3.
- pNn indicates that this device is on PCI bus M in slot N. So So1p40 is a WLAN card on PCI bus 4 slot 0. If the card is a multi-function device (possible with an Ethernet card with multiple ports, or devices that have Ethernet plus other functions), you may find en0s1f0 is function 0 of the Ethernet card in slot 0. There might also a second interface name en0s1f1 that is function 1 of that device.

Persistent naming means that once you know the name for a network interface on the system, you also know that it will not change. The trade off is that you cannot assume that a system with one interface name will translate eth0.

# IPV4 NETWORKING

IPv4 is the primary network protocol used on the Internet. You should have at least a basic understanding of IPv4 networking in order to manage network communication for your servers.

# IPv4 Addresses

An IPv4 address is a 32-bit number, normally expressed in decimal as four 8-bit octets ranging in value from 0 to 255, the address is divided into two parts: the network part and the host part. All hosts on the same subnet can talk to each other directly without a router, have the same network part; the network part identifies the subnet. No hosts on the same subnet can have the same host part; the host part identifies a particular host on the subnet.

In modern networking, the size of an IPv4 address is variable. To know which of an IPv4 address is the network part and which is the host, an administrator must know the netmask, which is assigned to the subnet. The netmask indicates how many bits of the IPv4 address are used. The more subnets available for the host, the more hosts are on the subnet.

The lowest possible address on a subnet (host part is all zeros in binary) is sometimes called the network address. The highest possible address on a subnet (host part is all ones in binary) is for broadcast messages in IPv4, and is called the hostcast address.

Network masks are expressed in two forms. The older syntax for a netmask uses 24 bits for the network part and reads 255.255.255.0. A newer syntax, CIDR notation, specifies a network prefix of /24. Both forms convey the same information; namely, how many leading bits in the IP address count to its network address.

RH124-RHEL8.0-en-1-20190507

391