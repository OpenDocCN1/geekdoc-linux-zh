
| Interconnect Type | Relative Performance: Bandwidth | Relative Performance: Latency | Point to Point Max Distance Supported in a NSPOF Config | Relative Cost | Slots Consumption | Redundancy Model | 1st Supported Release |
|---|---|---|---|---|---|---|---|
| Memory Channel | High | Low | 20 meters | High | 1 PCI slot/rail | Active/Passive | 5.0 |
| Memory Channel with Fibre Bridge | Medium | Medium | 6000 meters | High | 1 PCI slot/rail | Active/Passive | 5.0 |
| Fast Ethernet | Medium | Med/High | 1100 meters | Low | ¼ slot/rail (4-port card) | Active/Passive (NetRAIN) | 5.1A |
| Gigabit Ethernet | High | Med/High | 1100 meters | Med/High | 1 PCI slot/rail | Active/Passive (NetRAIN) | 5.1A |

**Table 3-1: Memory Channel Vs LAN Comparison**

### 3.3.3.1 Example

For the Biotech cluster, a dual-redundant Memory Channel cluster interconnect configuration will be used.

### 3.3.4 Should Network Interfaces be Highly Available?

If clients and users cannot access the cluster over network interfaces, it is as good as down. So yes, configure network interfaces for high availability.

How is it done? *TruCluster* Server solutions have mechanisms at two levels to insure that network connectivity stays up in the face of failure. At the first level, the *TruCluster* Server software’s Cluster Alias capability can be used. The cluster alias can be configured so that if a member’s network interface fails, another member with a working interface can act as a proxy, accepting and forwarding network traffic from the original member over the cluster interconnect. At the *Tru64* UNIX level, the NetRAIN and LAG⁵ interfaces provide a means to create a single logical IP interface from multiple physical network cards and remain highly available when one of the physical interface cards fail. You can read about NetRAIN and LAG in more detail in Chapters 9 and 12.

## 3.3.5 Default Basic Remedy to a Failed Network Interface on a Member - Using a CLUA Common-Subnet Alias

The Cluster Alias (CLUA) subsystem is a component of TruCluster Server software that allows virtual network addresses to be created and used to allow clients to connect to services in the cluster, independent of the member's native IP addresses and any failures to those interfaces or members. The Cluster Alias subsystem is described in detail in Chapter 16. Here we will briefly describe configuration options and alternatives when designing a cluster solution.

Using the Cluster Alias with the default, common subnet alias type, requires no special hardware beyond each member systems having a network interface to the public network, which would be the norm anyway. Under this configuration scheme, if the one network interface of a member currently receiving traffic from the outside world fails, then the Cluster Alias subsystem will automatically choose another member to receive incoming traffic on its interface on the same subnet and forward any traffic destined to the original host over the cluster interconnect to reach it. This scheme will meet most requirements by offering the following:

- Configuring member systems with only a single NIC to a public network, network traffic will be delivered to a member even when its single physical NIC to that network fails.

In rare cases, the routing incoming traffic over the cluster interconnect could cause the following issues:

- For some applications, the additional step of being rerouted over the cluster interconnect might result in an unacceptable performance impact.

- The additional traffic on the cluster interconnect could, in extreme cases, impact the ability of the cluster to use the cluster interconnect for other purposes, such as the Connection Manager subsystem and forwarding I/O for devices and file systems.

If you encounter a situation where you believe using the Alias is causing excessive traffic on the cluster interconnect, you can use software configuration options and additional hardware to minimize the effect. These methods are described next.

## 3.3.6 Additional Options That Eliminate Any Potential Network Traffic Being Re-Routed Over the Network Interconnect

As described in the previous section, using the default cluster alias with single network interfaces can result in undesirable network traffic on the cluster interconnect. If this is an issue for the cluster you are designing, you have four options.
