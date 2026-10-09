with packet filtering. Using both tools at once on the same machine will simply confuse you.

A packet filter compares every network packet that enters the system to a list of rules. When a rule matches the packet, the kernel acts based upon that rule. Rules can tell the system to allow, drop, or alter the packet. You can’t use the nifty options provided by TCP wrappers, however; instead of spitting a comparatively friendly rejection message back at the client, the connection is severed at the network level before the client even reaches the application.

While the idea of packet filtering is straightforward enough, your first implementation will be a complete nightmare—er, I mean, a “valuable learning experience.” Be prepared to spend hours experimenting and don’t be discouraged by failures. In my experience, its ignorance of basic TCP/IP that causes grief with packet filtering, rather than the packet filter itself. Trying to filter network traffic without understanding the network is frustrating and pointless. The only way to really understand TCP/IP is to do real work with it, however. Go study Chapter 7 again. If that doesn’t suffice, dig into the books recommended there.

FreeBSD suffers from a wealth of packet filters: IPFW, IP Filter, and PF.

IPFW is the primordial FreeBSD packet filtering software. It’s tightly integrated with FreeBSD; in fact, the generically named files /etc/rc.firewall and /etc/rc.firewall6 are purely for IPFW. While quite powerful and very popular with more experienced FreeBSD administrators, it’s a little difficult for a beginner.

The second packet filter, IP Filter, is not a FreeBSD-specific firewall program but is supported on several Unix-like operating systems. It’s primarily the work of one individual, Darren Reed, who has by heroic effort developed the overwhelming majority of the code and ported it to all those operating systems. IP Filter is most useful if you want to share one firewall configuration among multiple operating systems.

We’ll focus on the imaginatively named PF, or packet filter. PF originated in OpenBSD and was designed to be featureful, flexible, and