# So What Does the Routed Program Do?

The routing configuration described above is best suited to simple network arrangements where there are only ever single possible paths to destinations. When you have a more complex network arrangement things get a little more complicated. Fortunately for most of you this won't be an issue.

The big problem with “manual routing” or “static routing,” as described, is that if a machine or link fails in your network, then the only way you can direct your datagrams another way, if another way exists, is by manually intervening and executing the appropriate commands. Naturally this is clumsy, slow, impractical, and hazard prone. Various techniques have been developed to automatically adjust routing tables in the event of network failures where there are alternate routes; all of these techniques are loosely grouped by the term “dynamic routing protocols.”

You may have heard of some of the more common dynamic routing protocols. The most common are probably RIP (Routing Information Protocol) and OSPF (Open Shortest Path First Protocol). The Routing Information Protocol is very common on small networks such as small-medium sized corporate networks or building networks. OSPF is more modern and more capable at handling large network configurations and better suited to environments where there is a large number of possible paths through the network. Common implementations of these protocols are: “routed” - RIP and “gated” - RIP, OSPF, and others. The “routed” program is normally supplied with your Linux distribution or is included in the “NetKit” package detailed above.

An example of where and how you might use a dynamic routing protocol might look something like the diagram on the following page:

We have three routers A, B, and C. Each supports one Ethernet segment with a Class C IP network (netmask 255.255.255.0). Each router also has a PPP link to each of the other routers. The network forms a triangle.

It should be clear that the routing table at router A could look like:

```
root# route add -net 192.168.1.0 netmask 255.255.255.0 eth0
root# route add -net 192.168.2.0 netmask 255.255.255.0 ppp0
root# route add -net 192.168.3.0 netmask 255.255.255.0 ppp1
```