+   * Class B addresses include IP addresses from 128.0.0.0 to 191.255.255.255. The first 16 bits identify the network, and the last 16 bits identify the host.
+   * Class C addresses include IP addresses from 192.0.0.0 to 223.255.255.255. The first 24 bits identify the network, and the last 8 bits identify the host.
+   * Class D addresses include IP addresses from 224.0.0.0 to 239.255.255.255. They are used for multicasting (sending data to a number of destinations at once) and are not discussed here.
+   * Class E addresses range from 240.0.0.0 to 247.255.255.255 and are reserved for future use, as are addresses from 248.0.0.0 to 255.255.255.255.

# Background Material

The different classes of addresses have become less important with the advent of classless interdomain routing and subnetting. Subnetting is a further division of the host portion of the address into a subnet and host part.

As an example, The IP address 134.117.9.35 is a class B address with network part 134.117 and host part 9.35. Organizations may can choose to subdivide addresses. For example, the organization assigned the address block 134.117 might assign 134.117.1 as a class C network to one department, 134.117.2 to another department, and so on. Thus, The address 134.117.9.35 represents host number 35 on subnetwork 9 of network 134.117.

If you are setting up a network, you should use the size of the network to decide which class to use. Most small LANs have fewer than 254 hosts, so a class C network is adequate. Large organizations, which may require several interconnected LANs, might require a class B network. Very few organizations require class A networks.

# Private Addresses

Normally, IP addresses must be globally unique. They are assigned by a central authority called the Internet Network Information Center (InterNIC). However, certain blocks of addresses are reserved for private use. If you are setting up a network of machines that will not be connected to the Internet, you should use these private addresses. Even if you plan on Internet connectivity, you should use private addresses for internal hosts that you do not want seen from the outside world. The private network addresses are:

+   * Class A: 10.0.0.0. (All addresses beginning with 10.)
+   * Class B: 172.16.0.0 through 172.31.0.0. (All addresses beginning with 172.16 through 172.31.)