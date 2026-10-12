Look in the /etc/sysconfig/network-scripts directory for a file with a name that matches the name of the interface that should be saved.

# ## Configuring Routing

The routing panel configures the default gateway and adds static routes to the routing table. The Network Packet Forwarding (IPv4) option is provided to activate routing between networks that are configured on the system. If the system contains at least two interfaces, and IP traffic needs to be routed between these interfaces, check this option; otherwise it should be left unchecked. Actually, the choice to route is more involved than simply enabling this option. The selection and configuration of a routing protocol is necessary as well, but is beyond the scope of this book. By default, this feature is disabled. Figure 10.18 shows the routing panel.

![](bbox=[0.09, 0.47, 0.79, 0.76])

Figure 10.18  *Routing panel.*

The next two fields are used for the default gateway. The default gateway (or router) is used when a routing protocol such as RIP isn’t installed or configured on a system. Using a default router means that if any networks that are not explicitly defined within the routing table must be accessed, the default routing path is used.