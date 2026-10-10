
## OpenStack Management Network
OpenStack also has a concept of a management network. It’s one of several private networks in an OpenStack deployment and is used by the administrators to log into the machine to complete systems administration tasks. This network is also available for monitoring. Splitting out this network prevents system administration and system access monitoring from being impacted by traffic being used elsewhere in the deployment, such as bursts of API and compute instance traffic.

In the deployment scenarios in this book, we give our OpenStack nodes firewalled access to the Internet in order to allow for the installation of packages, Puppet modules and other sources required by the scenarios. This may also be what you do in production, but in a more secure environment access to all of your installation resources would be restricted to the local network. In this secure environment, you may host a local distribution package mirror, configuration management repositories, and netboot or system installation servers on your local management network. Doing so also allows you to stage and thoroughly test all the changes in packages and other resources stored on local mirrors before putting them into production.

## Control Plane
In networking terms, the control plane carries signaling traffic between network elements.

In OpenStack you may consider using a very similar control network. It would be the network where your messaging queue for interaction between services would live and any other traffic related to service interaction. For lieu of a dedicated management network, it’s common for management traffic to share the same private network as control traffic.

## Data Plane
Finally, there’s the data plane. This is where all of your actual network payload going to users and customers will be running. In OpenStack you can think of this as where instance traffic and public services like access to files in the Swift object storage are served up.

## Provider Network
A Provider Network is simply the logical representation of a network that is provided to OpenStack for use. This is not necessarily a different type of network from those mentioned above, but it has the distinction of being provided by a source outside of OpenStack and is marked as such. This source may be a switch or other network hardware or software that has control over the network you’re connected to. A provider network may map to a physical network, which may be a network that is routable within a data center or a network that is accessible to the Internet. It’s common to have multiple provider networks. Since provider networks are externally provided, configuring them in OpenStack is simply a matter of informing Neutron about basic data center network topology so it can use this information for the compute instances.

## Tenant Networking
An OpenStack deployment will typically have a series of Tenant Networks, which run on top of the data plane. Each instance connects to one or more tenant networks, where they will get their native IP address(es), which can be seen within the instance. By default, this address will only be locally routable between instances that exist in that tenant network and to specific services, such as the DHCP server used to assign those addresses and the router that may pass along that traffic to an external provider network.

Tenant networking for instances is where things get complicated. Traffic on tenant networks needs to be appropriately forwarded between instances; you generally want some kind of isolation, and in many deployments there is an allowance for overlapping subnets to be used as internal networks. OpenStack Neutron offers three options for handling traffic in the tenant network: flat, virtual local area network (VLAN) and tunneled.

### Flat Network
In a flat network, everyone shares the same network segment. No network segregation is applied nor any kind of tagging. This means that tenants can see the traffic from other tenants and the controller, plus address space cannot overlap. This decreases the amount of flexibility considerably, and if these are instances controlled by different parties, this is not an ideal situation. Use of flat networking is typically not advisable unless you fully understand the implications and limitations but could be reasonable in a small enterprise environment controlled by a single team and when external hardware resources are used extensively.

### Segmented Network
With flat networking behind us, we’re left with the other two options for handling traffic to focus on: VLANs and tunneling. In both of these scenarios, separation is provided, which also means that tenants can overlap in network subnet range, using the same local IP addresses without conflict. Whichever one you decide to use, it will be implemented via the Modular Layer 2 (ML2) plug-in with Open vSwitch (OVS) or Linux Bridge.

In this book we’ll be using the OVS model. OVS is often easier to use and more flexible than Linux Bridging. Neutron creates bridges within OVS, as well as internal VLANs. These internal VLANs that are created are entirely local to the node and use VLAN numbering that is distinct from the external segmentation IDs (such as VLANs outside the node). These internal VLANs exist even if you are not using external VLANs, such as if you are deploying a VXLAN-based topology.

### VLAN
In a VLAN network, each tenant is assigned to a VLAN. To support this environment, you must have hardware switches in your infrastructure that supports VLANs for each tenant network. This typically would be set up by using the tooling that comes with the switch or, if supported, allowing OpenStack to use a plug-in from that vendor (see the “Exploring the Possibilities with Neutron” sidebar in Chapter 5, “Foundations for Deployments”). This is particularly useful in a data center where VLANs are already used. It’s also useful if you have other hardware, such as a storage device, that you wish to include in your VLANs. You can also make use of external firewalls and routers to intelligently handle tenant traffic.

### Tunnelling
In a tunnel-driven network, encapsulation of traffic is used to provide separation. The most common encapsulation protocols are Generic Routing Encapsulation (GRE) and Virtual Extensible Local Area Networking (VXLAN). GRE and VXLAN are very similar, but VXLAN is more commonly used in cloud deployments because of its greater flexibility and efficiency. Using Neutron with OVS, a mesh of tunnels is set up between the OpenStack nodes in your environment. As traffic is sent along these tunnels, the Ethernet frame will be encapsulated in a new IP packet, which is routed to the destination node. The packet is then decapsulated and delivered into the appropriate instance (running on a compute node), control process (like DHCP running on the control node) or routed out of the tenant network (via a virtual router on the controller node or a physical router). See Figure 3.1 for an example of what a packet coming from an instance would look like.

Although the traffic is carried over the physical network, because it's encapsulated there is no visibility to the specific tenant network traffic from the perspective of the data center hardware. It just appears to be traffic between two OpenStack nodes.

It's worth noting that, in practice, it has generally been found that tunneling (such as GRE and VXLAN) scales better than VLANs. VLANs are more commonly found in an enterprise environment where the number of tenant networks is finite and the data center uses a common layer-2 switch fabric throughout. VLANs also require configuration of all your networking hardware to support each tenant and can run into limitations with regard to the number of VLANs that can exist on a given switch or link. Tunneling instead pushes complexity and scaling concerns into OpenStack, so it is not required on the data center network equipment. Using tunneling can also be easier to deploy and debug. When you go into production, you'll need to do an analysis of your own environment with your networking team to determine which method to use.

### Maximum Transmission Unit (MTU)
Before going any further, it's also important to take a moment to discuss Maximum Transmission Units (MTUs). If you refer to Figure 3.1, you will notice that this

![Figure 3.1](img/8684900d708748f86bb043faa5589f9e_67_0.png)
