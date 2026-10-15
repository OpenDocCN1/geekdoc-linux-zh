+   - Does it add new features that are needed by the organization now or in the near future?
+   - Does it fix any security holes?
+   - Does it increase performance significantly?

If you answered "yes" to any of these questions, a software upgrade should then be considered for your router systems.

Should you determine that the software is worth considering for an upgrade, you should investigate if there are any known interoperability issues with equipment in your environment. Issues of interoperability with the current software also should be investigated because upgrades must often be performed in phases.

# Technical Considerations for Router Efficiency

The most common technical consideration for effective router efficiency is the routing table or more specifically, the routing table size. A minimized routing table ensures efficiency in routing decisions because a smaller routing table speeds routing decisions. A minimized routing table also ensures efficiency in administration given that a smaller routing table is easier to troubleshoot by network administrators.

# Routing Tables in Static Routing Networks

Networks that use static routes will tend to be very efficient networks during the early stages of the network but will tend to become inefficient as changes are made to solve the specific network requirement without consideration of the complete network. The following tips, when applied to the complete network, will ensure networking tables maintain the minimum size necessary to support the network.

# Effective Use of Default Route

Probably the most underused feature among experienced and inexperienced network administrators is the use of the default route. While it is well understood that the default route is the route of last resort, many administrators are in the habit of creating routes on all routers when a new network is brought into service. This is typically unnecessary in most static route-based networks due to their simplicity and tendency to route towards the core of the network or a central router, which is in the patch for the new network.

Consider the network in Figure 10.1. When network 10.1.40.0/24 is brought online, many network administrators will tend to create routing entries for 10.1.40.0/24 at sites B, C, and D. However, because sites B, C, and D must use site A for transport to 10.1.40.0/24 and there is a pre-existing default route, adding a routing entry for 10.1.40.0/24 is an unnecessary routing entry.