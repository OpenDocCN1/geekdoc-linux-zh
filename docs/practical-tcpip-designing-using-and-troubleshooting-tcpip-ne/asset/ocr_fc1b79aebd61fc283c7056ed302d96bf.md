# ## 23.4 NAT – port translation; one-to-one NAT

![](bbox=[0.13, 0.1, 0.89, 0.43])

Figure 23.5 Port translation distinguishes between multiple connections

# ### Port translation

In our example network (Figure 23.5), all packets arriving from outside are addressed to 192.0.2.78; how does the NAT device decide which internal machine they are really destined for? It uses **network port translation** (*NPT*), also called **port address translation** (*PAT*) or **network address and port translation** (*NAPT*), to do this. (NAT is often assumed to include PAT – the usage of the terminology isn’t very strict.)

When an outgoing packet for a new combination of *source address* + *source port* passes through the NAT device, the device creates and stores a new mapping entry. Not only does it translate the source address, to 192.0.2.78 in Figure 23.5, but it also translates the source port – to a new port number that isn’t in use. E.g. port 456 on 10.1.1.1 is translated to port 9385. Now when a packet arrives from outside, addressed to 192.0.2.78, port 9385, the NAT device looks up the port number in its internal mapping table. It sees that 9385 really refers to port 456 on 10.1.1.1. translates the IP number and port accordingly, and passes the packet on to Alice. Similarly, when a packet arrives from outside addressed to 192.0.2.78 but on port 2167, the NAT device translates this to 10.2.2.2 port 456 and passes it to Bob.

In this way – dynamically mapping each combination of internal address and port to a unique outside port number on the same outside IP address – the NAT device can distinguish unambiguously between packets for any internal machine.

# ### Port translation and initiating connections from outside

How can Dave on the Internet initiate a connection, to an e-mail server, say, on Bob on the LAN? Specifying “destination IP = 192.0.2.78 port 25” doesn’t work, because Alice also