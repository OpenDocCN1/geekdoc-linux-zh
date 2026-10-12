interface. The **ipRouteType** object indicates the type of the route and includes the following values: **other** (1), **invalid** (2), **direct** (3), and **indirect** (4). The **ipRouteType** conveys the notion of **direct** and **indirect** routing. The **invalid** value invalidates the route, and **other** means that none of the other values list apply. The **direct** value means that the **destination** address is on a directly attached subnetwork, while **indirect** means the **destination** is not on an attached network but at least one additional route must be traversed before the **destination** can be reached. The **ipRouteProto** object indicates the mechanism used to learn the route. Table 6.4 lists the **ipRouteProto** values for an example in which the method used was **local**. This value means that the route was configured manually, without the aid of a routing protocol. This can be done, for instance when an interface is first initialized.

# Table 6.4 Defined ipRouteProto values

| ipRouteProto Value | Description |
|---|---|
| other | None of the following values |
| local | Routing information that is manually configured or derived from a nonrouting protocol source |
| netmgmt | Routing information obtained from a network management protocol |
| icmp | Feedback from hosts and other devices about a problem; provides a redirect message that gives specific routing information |
| egp | Exterior Gateway Protocol (EGP), which is described in RFC904; a simple router-to-router networking protocol |
| ggp | Gateway-to-Gateway Protocol; a routing protocol used by the early implementation of the Internet, but now obsolete |