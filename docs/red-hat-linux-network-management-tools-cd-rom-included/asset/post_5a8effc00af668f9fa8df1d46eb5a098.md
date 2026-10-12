
must now split the host portion and the subnet address from just one octet. However, the same procedure applies as stated above.

In order to formulate a subnet address from a class C network address, we must borrow some number of bits from the host portion of the address to represent the subnet number. In doing so, we automatically reduce the number of IP addresses that will be free for each device within the subnet. Therefore, we need to know exactly how many devices will be installed on the subnet. To further refine our example, assume we will only need ten IP addresses for individual nodes on the subnet.

We can determine the subnet mask and other information by hand, but it is much easier and faster if we use a software program to do the calculations for us. One excellent calculator is available from the Chesapeake Web Site (www.cci.com/tools/subcalc). This software provides the ability to subnet any valid IP address and shows us the calculations and steps involved. Figure 3.14 shows the main screen. Please note, this software can be downloaded and run from a local computer or executed directly from the Chesapeake site. Download and installation instruction for use on a local computer can be found in Appendix C.

![](img/f265c9d1f2610aca197c430cbfcd51f5_119_0.png)

Figure 3.14 Main subnet calculator window.

The first field, IP Host Address, requires that we specify the IP address of one of the hosts on our network. In this case, we give it one of the node addresses from our second example (i.e., 199.81.23.1). Next, we provide some information about the subnet by entering information in the third box, labeled "Select One of the Following". We can do this in one of four ways: by specifying the subnet mask directly (Subnet Mask field), the number of bits for the subnet (Bits field), the maximum number of hosts within the subnet (Maximum Possible Subnets field), or the number of possible hosts per subnet (Possible Hosts per Subnet field). Changing one of these fields changes the other three automatically. For example, when a subnet mask is changed to 255.255.255.224, then the number of bits becomes three and the number of possible hosts per subnet goes to 30.

The relationship between these fields can be more easily seen by viewing the calculations window shown in Figure 3.15. This screen contains five sections. The first shows two lines each containing three fields, the standard IP Address (Class C Network field) class in both decimal and binary format, the Subnet and Host bits fields respectively, and the subnet mask. This is the mask that must be applied to every system that will be involved within the subnet. This subnet mask uses 28 bits and hence can be referred to as a “28-bit subnet mask.” The second section contains the subnet number from the logical AND operation of the host address (199.81.23.1) and subnet mask (255.255.255.224) fields. The third shows the correct subnet mask, inverted subnet mask, and subnet number as expressed in binary. The next section contains the subnet directed address and the broadcast address. The broadcast address directs IP packets to every node on the local subnet. The final section includes the summary that contains the subnet address, the available host addresses specified with a range, and the directed broadcast address. The available host range is important because it represents the addresses that can be used by all host systems within the subnet.

## Internet Control Message Protocol

As previously discussed, IP provides a best-effort packet delivery mechanism that doesn't guarantee data delivery. IP is isolated from the lower-level protocol details and makes few assumptions about the performance and reliability of the network. Data delivery is accomplished without any special coordination among other IP entities and, for the most part, operates quite well. However, conditions might exist beyond IP’s control that make delivery difficult or impossible. For example, a remote host could be temporarily removed from the network or a router could become overloaded when a network-intensive application is started. IP needs a way to detect these types of problems.

The Internet Control Message Protocol (ICMP) provides a general error message facility for the IP protocol and related services. ICMP provides a way for IP entities that encounter errors to report them to the source that caused the problem. It is the responsibility of the source entity to correct the error. This might include, for example, reporting the error to a higher-level application. Table 3.6 lists some of the ICMP message types.

![](img/f265c9d1f2610aca197c430cbfcd51f5_121_0.png)

### Figure 3.15 Subnet calculation window.

**Table 3.6 ICMP error message types**

| Message Type | Meaning |
| :--- | :--- |
| Echo request/reply | Determine system reachability |
| Destination unreachable | Can't reach desired destination |
| Source quench | Stop sending data |
| Redirect | Detection of routing error |
| Time exceeded | Stale IP packet |

One of the most popular networking debugging utilities, `ping`, uses ICMP to determine host reachability. `ping` uses the echo request and echo reply primitives that are available within ICMP to determine if a remote host is available and operating correctly on the network. Figure 3.16 shows the basic operation of the echo request and reply. A user wants to determine if Node B is available on the network. From Node A, the user enters a `ping` command that issues an echo request to Node B. If Node B is active, it responds back to Node A using an echo reply. If Node B is not active, then Node A receives no response. In this case, the request from Node A simply times out. When this occurs, the user is presented with a time out message that indicates that Node B didn’t respond to the request.

![](img/f265c9d1f2610aca197c430cbfcd51f5_122_0.png)

### Destination Unreachable

When a router can’t deliver or forward a packet to its destination, it will emit an ICMP destination unreachable message to the sender. Destination unreachable errors usually imply some sort of routing problem or error (i.e., incorrect route within a routing table). Destinations may be unreachable due to hardware failures that cause a system to become temporarily unavailable, or when the sender specifies a non-existent destination address. Sometimes it is impossible to know that a destination is unreachable unless the ping system utility is used. For example, if a user issues a Telnet request to a remote system (which happens to be connected to an Ethernet LAN), and the system has been disconnected from the network, this Telnet request will eventually time out because Ethernet doesn’t support any frame acknowledgments. As a result, no destination unreachable messages will be generated because Ethernet assumes data delivery even for a node that has been temporarily disconnected from the network.

### Source Quench

The source quench within ICMP provides a way to handle congestion at the IP packet level. Congestion within a network can be caused by several factors. However, one primary cause is when several systems begin transmission of data that flows through a single router, as shown in Figure 3.17. In this case, the router itself is overloaded by the combined traffic. Another cause of congestion is when a more powerful computer system transmits data to a less powerful system that cannot keep up the pace. If these situations go unchecked, eventually the router and under-powered system will begin to discard packets, which in turn will cause TCP to retransmit them, thus making the situation worse. In this case, the router and smaller system simply emit a source quench message, which indicates to the sender that it should stop sending data. As a result, the router and smaller system have time to process any outstanding packets.

There is no direct way to reverse the effects of the ICMP source quench message. However, any destination that receives a source quench lowers the rate at which it transmits packets to the destination. After no additional source quench messages are received, the
