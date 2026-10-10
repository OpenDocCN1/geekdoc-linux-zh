# IPFW Packet Traversal

Under IPFW (ipfwadm and ipchains), three built-in filter chains were used. All packets arriving on an interface were filtered against the input chain. If the packet was accepted, it was passed to the routing module. The routing function determined whether the packet was to be delivered locally or forwarded to another outgoing interface. IPFW packet flow is pictured in Figure 3.1.

![](bbox=[0.1, 0.24, 0.95, 0.48])

If forwarded, the packet was filtered a second time against the forward chain. If the packet was accepted, it was passed to the output chain.

Both locally generated outgoing packets and forwarded packets were passed to the output chain. If the packet was accepted, it was sent out the interface.

Received and sent local (loopback) packets passed through two filters. Forwarded packets passed through three filters.

The loopback path involved two chains. As shown in Figure 3.2, each loopback packet passed through the output filter before going “out” the loopback interface, where it was then delivered to the loopback’s input interface. Then the input filter was applied.

Note that the loopback path demonstrates why people’s X Window session hangs when starting a firewall script that either doesn’t allow loopback traffic or fails before doing so when a deny by default policy is used.

In the case of response packets being demasqueraded before forwarding them on to the LAN, the input filters were applied. Rather than passing through the routing function, the packet was handed directly to the output filter chain. Thus, demasqueraded incoming packets were filtered twice. Outgoing masqueraded packets were filtered three times.