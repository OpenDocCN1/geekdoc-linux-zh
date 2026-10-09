other hosts without involving a router is called a broadcast domain, or segment.

Ethernet segments are connected via hubs or switches. An Ethernet hub is a central piece of hardware to physically connect many other Ethernet devices. Hubs simply forward all received Ethernet frames to every other device attached to the network. Hubs broadcast all Ethernet traffic that they receive to every attached host and other attached hubs. Each host is responsible for filtering out the traffic it doesn’t want. Hubs are old-school Ethernet and rarely seen today.

Switches have largely supplanted hubs. A switch is like a hub, but it filters which traffic it sends to each host. It identifies the physical addresses of attached devices and, for the most part, forwards frames only to the devices they are meant for. Since each Ethernet host has a finite amount of bandwidth, switching reduces the load on individual systems by decreasing the amount of traffic each host must sort through.

# ## Switch Failure

Switches fail, despite what Cisco would have you believe. Some failures are obvious, such as those where the magic black smoke is leaking out of the back of the box. When a switch loses its magic smoke, it stops working. Others are more subtle and make it appear that the switch is still working.

Every switch manufacturer must decide how to handle subtle errors. Either the switch can shut down until it is attended to, or it can attempt to alert its manager and continue forwarding packets to the best of its ability. If you’re a vendor, the choice is obvious—you stumble along as best you can so your customers don’t think your switches are crap. This means your switch can start to act like a hub and you might not know about it. The bad news is that if you were relying on the switch to prevent leakage of secure information, you’re fated for disappointment. More than one switch has failed on me in this way, so don’t be too surprised when it happens to you.