
- **RIP**— The Routing Information Protocol is the interior protocol most commonly used on UNIX systems. It makes routing decisions based solely on the results of applying a distance-vector algorithm to route metrics, or hop counts. It is simple to configure, and it is adequate for most small-to-medium networks.

RIP has some serious shortcomings for large-scale use. It limits network diameter to 15 hops. It exhibits *slow convergence*—it may take up to 180 seconds for the routing table to reflect the new situation if previously correct routes become invalid. Also, it is unaware of classless IP addresses—all RIP routes must be for addresses that use their natural mask.

- **RIP-2**— This is the Routing Information Protocol Version 2. It is a backwards-compatible version of RIP, using fields in the RIP packet that were reserved for future extensions. RIP-2 fixes most of the problems with RIP, and also adds features such as authentication for routing information.

- **OSPF**— Like RIP, Open Shortest Path First is an interior protocol, but it differs significantly in that it is a *link-state protocol*. Where RIP routers share information about the entire AS with their neighbors, OSPF routers share information about their neighbors with the entire AS. This enables them to build a model of the entire network, and to use Dijkstra's well-understood shortest-path algorithm to determine the best route.

- **BGP**— The Border Gateway Protocol is the most common exterior routing protocol in use on the Internet. BGP supports policy-based routing; that is, the use of non-technical considerations such as security, cost, and organizational matters when making routing decisions. BGP learns the entire end-to-end path of a route, to ensure that routing loops do not occur.

## Miscellaneous Protocols

Other protocols have been used elsewhere, but are not common. They include the Hello protocol (which was used on the original 56 kbps NSFNET backbone) and IS-IS, the Intermediate System to Intermediate System protocol (which was used on the NSFNET T1 backbone). Both of these are interior protocols. The Exterior Gateway Protocol is an exterior protocol that was once common, but it relied on a central authority to determine the "best" routes, and it therefore scaled poorly in the face of the Internet's exponential growth. For this reason, it is seldom used nowadays.

Although there are many routing protocols, it is usually easy to select the right one in any given situation. For local area networks, RIP or RIP-2 is still the most common choice, and often its simplicity makes it a sensible one. The more complex algorithms in OSPF make it appropriate for larger networks.

Very few systems need to run exterior protocols: they are needed only when one AS must exchange routing information with another AS. Large Internet service providers are one of the few environments where exterior protocols are necessary. When an exterior protocol is necessary, there is rarely a choice as to the routing protocol used: If the other AS is already in operation, its administrators have almost certainly selected a routing protocol, and autonomous systems must run the same protocol to be able to exchange routing information.

## Routing Daemons

There are two main routing daemons that run on UNIX-like systems: routed (pronounced “route-dee”) and gated (“gate-dee”). Of these, routed is easier to configure, but being older, it also suffers from a lack of flexibility—it can only handle RIP. The gated daemon can handle RIP, RIP-2, OSPF, and BGP, as well as Hello and EGP.

To enable routed under Red Hat, you must first install the relevant RPM package. Then to arrange for it to be started at boot time, you can either use the Control Service Activity dialog in Linuxconf, or run the equivalent command by hand:

```
chkconfig routed on
```

To start or stop the service other than at startup or shutdown time, run one of these commands:

```
/etc/rc.d/init.d/routed start
/etc/rc.d/init.d/routed stop
```

Some configuration of routed can be performed with Linuxconf, as shown in Figure 14.7.

The default Red Hat configuration is for routed to listen to routes advertised by other systems but not to advertise routes itself; this is accomplished by starting routed with the -q switch. The other option in this dialog determines whether routed should advertise its default route (the -g switch). This is used on gateways to the Internet, or on gateways using another routing protocol whose routes are not advertised to other local routers. This setting defaults to off.

The routed daemon reads the /etc/gateways file at startup and uses the information within it to configure the routing table. It is not necessary to use this file, because the RIP messages received from other routers will be enough to let routed build a functioning routing table. But there are situations in which it is useful: perhaps to supplement the RIP information with an initial default route, or with information about a gateway that does not advertise its routes.

## Figure 14.7
Configuring routed with Linuxconf.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_426_0.png)

All entries in the /etc/gateways file have basically the same format, and that format is very similar to the command line for route, so it should be easy. Each entry is a single line containing the following items:

1. One of the words net or host to indicate whether the destination is to be treated as a network or a host.
2. The destination address, or 0.0.0.0 for the default route.
3. The word gateway.
4. The gateway's address.
5. The word metric.
6. The route's numeric metric value. This can be specified with route when adding a static route, but is essentially meaningless in that situation. RIP uses the metric as the cost of the route, so it prefers routes with lower metric values. For RIP, the metric should represent the number of gateways through which data must pass to reach the given destination, but it is actually an arbitrary value chosen by the administrator. If there is only one route to a given destination, that route should have a metric of 1.
7. One of the keywords active, passive, or external. Passive routes effectively become permanent static routes: They are not deleted by RIP, and they are not included in RIP information transmitted. Active routes, on the other hand, are advertised and updated by RIP. If no updates are received for an active route in a given period of time, it will be deleted from the routing table. External routes are similar to passive routes, but routed will not add them to the routing table. The external declaration indicates that some other routing protocol will install a route for the destination in question, and that routed should not install alternative routes for the same destination.

## Complex Routing Scenarios

More complex routing scenarios must be handled by the more flexible program gated. As you have already seen, gated can handle multiple routing protocols. It combines routing information learned from different protocols and selects the best routes available. It can advertise on exterior protocols routes whose existence was discovered by interior protocols, so reachability information announced externally can be adjusted dynamically to changing interior routes. It supports routing policies to control acceptance and advertisement of routes.

Perhaps most convenient of all for the administrator is that gated is configured from a single file (/etc/gated.conf) with a consistent syntax. There is also a group, the Gated Consortium (http://www.gated.org), which actively maintains it, so you can expect that bugs will be fixed and new features added.

## Running gated

When gated runs, it acquires routing information from multiple protocols; if it receives routes to the same destination from different protocols, it attempts to select the best one. This is not a trivial task because metrics used by different protocols are not directly comparable. The solution adopted in gated is to use configurable preferences. The administrator can use these preferences to prefer routes from one interface over another, or from one protocol over another, or from one remote gateway over another.

Enabling gated under Red Hat is very similar to enabling routed. You can enable it from the Control Service Activity dialog in Linuxconf, or you can run

```
chkconfig gated on
```

by hand (as root). To start or stop the service other than at startup or shutdown time, run one of the following:

```
/etc/rc.d/init.d/gated start
/etc/rc.d/init.d/gated stop
```
