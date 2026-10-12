short. Second, IP classes resulted in too many routing table entries. As a result, routers were becoming overloaded with information.

The Classless Inter-Domain Routing addressing scheme set out to deal with these problems. The scheme is similar to IP address classes, but offers much more flexibility in assigning how much of the 32-bit IP address is the network identifier. Instead of the first 8, 16, or 32 bits identifying the network, 13 to 27 bits could identify the network. As a result, groups of assigned IP addresses could contain from 32 to about 524,000 host addresses.

To indicate the network identifier, a CIDR IP address is followed by a slash (/) and then a number from 13 to 27. A smaller number indicates a network containing more hosts. Here is an example of an IP address that uses the CIDR notation:

128.8.27.18/16

In this example, the first 16 bits (128.8) represent the network number, and the remainder (27.18) represents the specific host number. This network number can contain up to 65,536 hosts (the same as a class B address). The following list shows how many hosts can be represented in networks using different numbers to identify the network:

+   /13 524,288 hosts
+   /14 262,144 hosts
+   /15 131,072 hosts
+   /16 65,536 hosts
+   /17 32,768 hosts
+   /18 16,382 hosts
+   /19 8,192 hosts
+   /20 4,096 hosts
+   /21 2,048 hosts
+   /22 1,024 hosts
+   /23 512 hosts
+   /24 256 hosts
+   /25 128 hosts
+   /26 64 hosts
+   /27 32 hosts

The CIDR addressing scheme also helps reduce the routing overload problem by having a single, high-level route represent many lower-level routes. For example, an Internet Service Provider could be assigned a single /13 IP network and assign the 500,000-plus addresses to its customers. Routers outside the ISP would only need to know how to reach the ISP for those half-million addresses. The ISP would then be responsible for maintaining routing information for all of the host routes with that network address.

# Getting IP addresses

So, what is the impact of assigning IP addresses for the computers on your LAN? How you choose which IP addresses to use depends on your situation. If you are part of a large organization, you should get addresses from your network administrator. Even if you don't