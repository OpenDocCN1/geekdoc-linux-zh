![](bbox=[0.45, 0.12, 0.6, 0.29])

My IP address is 10.2.0.4

Other computers on the network communicate with me by using this IP address.

They see my IP address in binary, which is 00001010 00000010 00000000 00000100

You cannot simply assign computers on your network any IP address you choose. The IP addressing scheme you use must be defined by classes and subnets. Just as everyone in a certain town has the same addressing properties of city, state, and zip code, the IP addresses must belong to certain classes and subnets. An isolated LAN or WAN can determine a class of addresses and appropriate subnet masks to use for their network, but for proper Internet communication, many networks choose to obtain IP addressing from Network Solutions, which is the organization that handles all of the Internet's domain name and IP address assignment.

Each IP address identifies both the network in which the computer (or node, such as a router) resides and the actual computer or node itself. These are called the network ID and host ID. The three major groupings of IP addresses are called classes. The following list gives you an overview of the three classes:

+   - Class A: Class A addresses have a beginning octet from 1 to 126. Network Solutions assigns the first octet and the network administrator assigns the three remaining octets. Class A networks were developed for large networks and obtaining a Class A address today is very difficult. Class A networks can support up to 16,387,064 hosts.
+   Also, the address range of 127 is reserved for TCP/IP troubleshooting and is called a loopback address.

+   - Class B: Class B networks have the first octet assignment from 128 to 191. Network Solutions assigns the first and second octet numbers and the network administrator assigns the last two. Class B networks can support up to 64,516 hosts.

+   - Class C: Class C networks use 192 through 255 for the first octet. Network Solutions assigns the first three octets and the network administrator assigns the final octet. Class C networks can only support up to 254 hosts.