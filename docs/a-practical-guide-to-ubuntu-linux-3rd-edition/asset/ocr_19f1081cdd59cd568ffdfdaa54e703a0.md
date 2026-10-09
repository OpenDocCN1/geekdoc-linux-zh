bits (100), 21 netid bits (2 million networks), and 8 hostid bits (254 hosts). Today a new large customer will not receive a class A or B network but is likely to receive a class C or several (usually contiguous) class C networks, if merited.

Several other classes of networks exist. Class D networks are reserved for **multi-cast** (page 1161) networks. When you run `netstat -nr` on a Linux system, you can see whether the machine is a member of a multicast network. A 224.0.0.0 in the Destination column that `netstat` displays indicates a class D, multicast address (Table 10-2). A multicast is like a broadcast, but only hosts that subscribe to the multicast group receive the message. To use Web terminology, a broadcast is like a “push.” A host pushes a broadcast on the network, and every host on the network must check each packet to see whether it contains relevant data. A multicast is like a “pull.” A host will see a multicast only if it registers itself as subscribed to a multicast group or service and pulls the appropriate packets from the network.

**Table 10-3** Computations for IP address 131.204.027.027

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| | **-----------Class B-----------** | | **netid** | **hostid** |
| | 131 | .204 | .027 | .027 **decimal** |
| **IP address** | 83 | CC | 1B | 1B **hexadecimal** |
| | 1000 0011 | 1100 1100 | 0001 1011 | 0001 1011 **binary** |
| | 255 | .255 | .255 | .000 **decimal** |
| **Subnet mask** | FF | FF | FF | 00 **hexadecimal** |
| | 1111 1111 | 1111 1111 | 1111 1111 | 0000 0000 **binary** |
| **IP address bitwise AND** | 1000 0011 | 1100 1100 | 0001 1011 | 0001 1011 |
| **Subnet mask** | 1111 1111 | 1111 1111 | 1111 1111 | 0000 0000 **binary** |
| **= Subnet number** | 1000 0011 | 1100 1100 | 0001 1011 | 0000 0000 |
| | 131 | .204 | .027 | .000 **decimal** |
| **Subnet number** | 83 | CC | 1B | 00 **hexadecimal** |
| | 1000 0011 | 1100 1100 | 0001 1011 | 0000 0000 **binary** |
| | 131 | .204 | .27 | .255 **decimal** |
| **Broadcast address** | 83 | CC | 1B | FF **hexadecimal** |
| **(set host bits to 1)** | 1000 0011 | 1100 1100 | 0001 1011 | 1111 1111 **binary** |

Table 10-3 shows some of the computations for the IP address 131.204.027.027. Each address is shown in decimal, hexadecimal, and binary form. Binary is the easiest to work with for bitwise (binary) computations. The first three lines show the IP address. The next three lines show the **subnet mask** (page 1175) in three bases. Next the IP address and the subnet mask are ANDed together bitwise to yield the **subnet number** (page 1175), which is shown in three bases. The last three lines