# TCP/IP Networking 83

Some hosts have a more or less permanently assigned IP address, called a static IP address. Other hosts are assigned a temporary IP address, called a dynamic IP address. Dynamic IP addresses are commonly used for mobile hosts, such as laptops, and for dial-in clients. Hosts that provide services to other hosts are generally assigned a static IP address so that clients will be able to refer to them using a consistent IP address. As you will see later in the chapter, IP addresses are a somewhat scarce commodity. Dynamic IP addresses require an IP address pool only as large as the number of active hosts rather than the total number of hosts.

# Network Classes

Organizations don't ask the Internet authorities to assign them a single IP address. Instead, they request a consecutive series of IP addresses that can be assigned to hosts within their network. The IP addresses are chosen from one of three classes, distinguished by the first octet:

+   * 100.0.0.0–126.0.0.0 Class A network addresses
* 128.0.0.0–191.0.0.0 Class B network addresses
* 192.0.0.0–223.0.0.0 Class C network addresses

An IP address consists of two parts: a network address and a host address. The network address is common to all directly connected hosts that compose a network. The host address distinguishes one individual host from the others on its network. The network address is taken from the high-order bits of the IP address, and the host address is taken from the lower-order bits. The size of the network address varies according to the network class:

+   * Class A 8 bits (1 octet)
* Class B 16 bits (2 octets)
* Class C 24 bits (3 octets)

Because the network address of a class A is only 8 bits long, 24 bits are available to specify host addresses. In contrast, the network address of a class C network is 24 bits long; only 8 bits are available to specify host addresses. Thus, a class C network can include only 254 hosts (the IP addresses and xxx.xxx.xxx.255 assigned to the network, so only IP addresses xxx.xxx.xxx–1–xxx.xxx.254 are available for hosts).

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com