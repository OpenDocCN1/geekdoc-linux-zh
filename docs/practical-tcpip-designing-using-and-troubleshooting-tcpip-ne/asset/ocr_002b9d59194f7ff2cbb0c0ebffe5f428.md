+   • each router has its own real IP and MAC address, as usual. These are used for managing the routers, and for the routers to talk to one another.
+   • the master also responds to the “virtual router” IP and MAC addresses, 192.0.2.254 and *a:b:c:d:e:f*, say, for our example
+   • the master and backup constantly talk to each other using VRRP, each checking that the other is up and running
+   • in normal running, the backup router performs no routing function – none of the LAN machines forward it any packets to route.
+   • when the master router fails, the backup router detects this and takes over the routing function. It will now respond to the virtual router IP address 192.0.2.254 and the virtual router MAC address *a:b:c:d:e:f*, exactly the same as the master router. The LAN machines don’t even know that this has happened, and the LAN users function as normal. The typical length of interruption on the network – before the backup takes over the routing – is less than a second.

The above is an over-simplification of VRRP. In practice you would probably share the load across both routers, using each as the backup for the other. You can have more than two routers, and you can connect each to more than one Ethernet switch so that you don’t have a switch as a single point of failure either.

# A cheap backup Internet connection

VRRP and high-availability switch configurations are too expensive and complex for most small and medium sites. A cheaper approach is to use a cheap cable modem or ADSL connection as backup for your primary connection (Figure 23.13). This only works if you’re using NAT provided by a box (e.g. firewall) behind the router, i.e. if your LAN IP addresses don’t depend on your external router address. When your primary connection fails, manually switch the firewall connection from the primary router to the ADSL router, and change the firewall’s default gateway accordingly. This only takes five minutes, but gives you a very usable backup, at very little cost and you can use different ISPs for your two connections, to give an extra level of backup. (Of course your public servers – which use IP addresses from your primary ISP – will not be visible over the backup line; but see the Notes for a possible solution.)

![](bbox=[0.2, 0.68, 0.7, 0.9])

Figure 23.13 Using ADSL as a cheap backup connection for your main Internet connection