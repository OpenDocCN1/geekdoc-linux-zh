a specific host. That means that anyone who breaks into a trusted host can immediately gain access to your protected network.

+   - Because it's based on IP addresses, packet filtering can be defeated by a technique known as *IP spoofing*, whereby a cracker sends packets with the IP address of a trusted host (by appropriating the IP address of a trusted host and setting up an appropriate route); packets with these fake IP addresses can then gain access to your system.
+   - Packet filtering is susceptible to routing-attack programs that can create a bogus route, allowing an intruder to receive all packets meant for the protected internal network.
+   - The screening routers that implement packet filtering don't keep logs of activities. That makes it hard for you to determine if anyone is attempting to break into the protected network. As you see in the next section, a dual-homed host can provide logging.
+   - A screening router does not hide the host names and IP addresses of the internal network. Outsiders can access and use this exposed information to mount attacks against the protected network.

A more sophisticated approach is to use an application gateway that controls network traffic, based on specific applications instead of on a per-packet basis. You can implement an application gateway with a dual-homed host, known also as a *bastion host*.

# Dual-homed host

A *dual-homed host* is a system with two network interfaces — one connected to the Internet and the other on an internal network that needs protection. The term “dual-homed” refers to the fact that the host “lives” in two networks.

In fact, if your operating system supports IP routing — the ability to forward network packets from one interface to another — the dual-homed host can serve as a router. However, you must turn off the IP forwarding feature to use the dual-homed host as a firewall system.

The Linux kernel supports the IP forwarding feature. If you plan to use a dual-homed host as a firewall, you have to use the `sysctl` command to disable IP forwarding.

With IP forwarding turned off, systems on both networks — the internal network as well as the Internet — can reach the dual-homed host, but no one from the Internet can access the internal network (nor can anyone from the internal network access the Internet). In this configuration, the dual-homed host completely isolates the two networks. Figure 3-2 shows the basic architecture of a dual-homed host.