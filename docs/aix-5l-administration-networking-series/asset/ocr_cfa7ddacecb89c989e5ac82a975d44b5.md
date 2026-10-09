local address, the system is able to send traffic on the local network. It can now send router solicitations on each of its local networks, and receive router advertisements telling it which prefixes it should use to configure its site local and global addresses. This allows new hosts to be added to a network without requiring each one to be configured manually. All the routers require special configuration.

On AIX 5L, the **autoconf** command can be used to configure interfaces with link local IPv6 addresses. The **nwdp-host** daemon, when run on a host, will send router solicitation packets and process any router advertisements that are received. The **nwdp-router** daemon should be run on IPv6 routers to cause them to send router advertisements. **nwdp-router** can be configured so that the router will advertise the correct prefixes and routers for the network it is on.

# ## Aliasing

It is possible for a network interface to have multiple addresses associated with it. This is known as aliasing. An interface can have multiple IPv4 with multiple IPv6 addresses concurrently. Aliasing can be useful when numbering a network; it may be desirable to assign the new address to the interface while keeping the old one during the transition time. When using IPv6, it is common for interfaces to have multiple addresses of different scopes, for example, a link local address and a global address.

Use the SMIT FastPath **smit inetalias** to configure aliasing on AIX 5L.

# ## VIPA

A virtual IP address (VIPA) is an address that is not associated with a particular physical network adapter. VIPAs can be used in situations where network communications might need to continue even in the event of a network interface going down. AIX 5L allows an administrator to configure an interface called **vio0** and assign an address to it. This address will be used as the default source address for any packets sent unless the application is explicitly bound to a different address. Using this mechanism, if the interface that was used to send the traffic is disabled, communication can continue using a different interface as long as there is still a route that allows traffic to reach its destination. Using a VIPA requires that the neighboring routers in the network be configured to be able to route responses back to the correct host. This could be done either by manually configuring the routers or by running the **gated** application on the host with the VIPA. **gated**, when configured to use the OSPF protocol, will automatically advertise information about the VIPA to neighboring routers.

# # NETWORK ROUTING

In IP routing, a system sending packets does not need to have complete information about where in the network every destination resides. Instead, it only needs to know the next hop to send to in order to get the packet closer to its destination. The next hop system is then responsible for knowing where to send the packet next.