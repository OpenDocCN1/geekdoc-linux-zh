
network bits for 192.168.240.0/21 are nnnnnnnn.nnnnnnnn.nnnneeee.hhhhhhhh, and if an f is used to represent this subnet, then there are two choices:

- Eight subnets will require three more bits and give me nnnnnnnn.nnnnnnnn.nnnnefff.hhhhhhhh or /24.
- Sixteen subnets will require four more bits—including those used for the eight subnet option—and give me nnnnnnnn.nnnnnnnn.nnnnefff.fhhhhhhh or /25.

Because eight has been chosen, the first of the eight subnets is 192.168.241.0/24 (nnnnnnnn.nnnnnnn.nnnne001.hhhhhhhh)—where we already know that the third bit’s nnne is 240. The full list of eight subnets is detailed in Table 4.7.

## Table 4.7 The Eight Campus Subnets Taken from Network 192.168.240.0/21, with Only the Changing Bits Displayed

| Subnet | Bit-wise | Network |
|---|---|---|
| Ag | .nnne000.hhhhhhhh | 192.168.240.0/24 |
| Eng | .nnne001.hhhhhhhh | 192.168.241.0/24 |
| Phys | .nnne010.hhhhhhhh | 192.168.242.0/24 |
| Hum | .nnne011.hhhhhhhh | 192.168.243.0/24 |
| Arts | .nnne100.hhhhhhhh | 192.168.244.0/24 |
| Chem | .nnne101.hhhhhhhh | 192.168.245.0/24 |
| Math | .nnne110.hhhhhhhh | 192.168.246.0/24 |
| spare | .nnne111.hhhhhhhh | 192.168.247.0/24 |

In each subnet, you get 254 addresses—if this seems like a class C to you, it is; a class C is just a /24 network. From here, you can actually subnet further for different departments or whatever suits your needs.

On the dorm side there are six buildings. This means once again that if you want one subnet per building, the closest you can get is eight. The dorm network is 192.168.248.0/21. Its eight subnets are calculated exactly the same way, and the results are given in Table 4.8.

## Table 4.8 The Eight Dorm Subnets Taken from Network 192.168.248.0/21, with Only the Changing Bits Displayed

| Subnet | Bit-wise | Network |
|---|---|---|
| Runik | .nnne000.hhhhhhhh | 192.168.248.0/24 |
| East | .nnne001.hhhhhhhh | 192.168.249.0/24 |
| Trud | .nnne010.hhhhhhhh | 192.168.250.0/24 |
| Wash | .nnne011.hhhhhhhh | 192.168.251.0/24 |
| Wall | .nnne100.hhhhhhhh | 192.168.252.0/24 |
| Poin | .nnne101.hhhhhhhh | 192.168.253.0/24 |
| spare | .nnne110.hhhhhhhh | 192.168.254.0/24 |
| spare | .nnne111.hhhhhhhh | 192.168.255.0/24 |

In this case, you might decide to have a subnet for each floor in the dorm or not make any subnetworks at all. Figure 4.4 shows you what our new network-addressing scheme looks like.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_97_0.png)

Figure 4.4 The current hierarchical Classless IP v4 networking scheme.

## Classless IPv4 Routing Issues

It might sound like Classless IP v4 puts a huge burden on the Internet's routers. Even worse, it could explode the routing tables into an unmanageable size that slows down all Internet traffic. Fortunately this is not the case. Not only does Classless IP v4 allow you to create subnets of subnets of subnets, it also allows you to hide the layers from the outside world—if you plan your network correctly. See Chapter 7, "Planning Router Layout and Function," for further information.

A well-planned VLSM setup includes route aggregation, a concept that allows you to hide subnetting from the outside world. Let me break down the VLSM subnets created in the previous section, "Applying Classless IP v4 Addressing Across Subnets," to demonstrate this concept. Each of the subnet layers was mathematically derived from

its parent layer. We started with the overall network 192.168.240.0/20. The 20-bit mask translates to nnnnnnnn.nnnnnnnn.nnnnhhhh.hhhhhhhh, where n is a network bit and h is a host bit. This means that you have access to the address range 192.168.240.0 through 192.168.255.255.

The two subnets within this network are 192.168.240.0/21 and 192.168.248.0/21. Both of these network addresses are within the main network’s address range. Therefore, no matter which subnet the traffic ultimately needs to go to, it first has to go to network 192.168.240.0/20 according to how the IP v6 routing works. No router outside the main university router (prime) needs to know that there are any subnets at all.

Our major subnets have their own address ranges. The campus subnet, 192.168.240.0/21, has the bit mask nnnnnnnn.nnnnnnnn.nnnnehhh.hhhhhhhh. This gives it the address range 192.168.240.0 through 192.168.247.255. The dorm subnet, on the other hand, is 192.168.248.0/21 and gets 192.168.248.0 through 192.168.255.255. Take a look back at Tables 4.7 and 4.8. Every network address listed there falls within one of these two major subnets’ available address ranges. Therefore, every network address in the campus and dorm buildings can be sent just to the main router, then to just the campus or dorm router, then to the appropriate building, and then directly to the correct machine.

In each case, only the router above the subnet layer needs to know that there are subnets involved at all. This is a good example of route aggregation, a term mentioned earlier. It is also the key to CIDR success. The more routing information that we can keep hidden at local levels, the smaller the overall routing tables need to be.

Routers under Classless IP v4 must carry information that IP v4 routers simply would not understand. While Classful IP v4 requires the netmask, Classless IP v4 needs the bit mask. The technique the routers use from that point is called longest match. The router looks at the address the information is trying to get to—let’s say 192.168.250.52—and looks for the entry in its routing table that is closest to this number. The best it’s going to find in a main routing table in this case is 192.168—remember that our parent network (the supernet) is 192.168.240.0/20.

Longest match isn’t well demonstrated at the beginning. Rather than sending the data to 192.168.0.0, the router trying to send the data to 192.168.250.52 will have to look up 192.168.240.0/20 in the routing tables unless all of 192.168.0.0 is owned by a single ISP that then hands out parts of the addressing to others. Let’s say that this is the case. The packet meant for 192.168.250.52 gets sent to the ISP that owns 192.168.0.0.

When the packet arrives at the ISP’s routers, they don’t see a longest match for 192.168.250.x. They do have 192.168.240.0/20 in their routing tables, however, so off the packet goes to our router Prime. Prime doesn’t have a longest match for 192.168.250.x either. However, it has in its routing tables that the network 192.168.248.0/21 exists, so now the packet is sent to router East.
