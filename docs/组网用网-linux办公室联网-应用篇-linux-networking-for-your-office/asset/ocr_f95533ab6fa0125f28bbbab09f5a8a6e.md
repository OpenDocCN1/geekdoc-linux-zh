+   - How many firewalls? If your network is small, one may suffice. You might want several firewalls, though, to protect separate portions of your organization’s network.

One of the most important decisions you’ll have to make is whether to use a "canned" firewall product or custom configure a Linux (or some other) system to serve as a firewall. A packaged product is certainly easier to configure, and will probably provide superior protection if you’re not already familiar with firewalls. Doing a custom configuration will help you get precisely the protection you need, but will cost more in time, especially if you must first learn the details of firewall configuration.

# CAUTION

> I cannot do more than provide the briefest overview of firewall principles and Linux firewall tools in this chapter. If you want to learn more, you can begin with the Linux Firewalling and Proxy Server HOWTO, which comes with Red Hat and other Linux distributions. From there, you can read the chapters on firewalls in books such as Sams’ Maximum Linux Security, or the New Riders title Linux Firewalls by Robert Ziegler.

# Using Multiple Firewalls in One Network

Many networks can benefit from the presence of two or more firewalls of various types, as illustrated in Figure 21.3. In this configuration, a packet filter blocks the most outrageous connection attempts based on packet analysis. Any traffic coming into the network is then passed directly to the proxy server, which can function as a mail relay, news server, and so on. Outgoing traffic passes through the proxy server, and then through the packet filter. Note that both incoming and outgoing traffic can be blocked at either firewall.

# Single- and Multi-Homed Firewalls

In Figure 21.3, both the packet filter and the proxy server are multi-homed, meaning that they possess two network interfaces and perform firewall functions to bridge those two interfaces. All other things being equal, a multi-homed firewall is more secure than a single-homed firewall. For instance, in the network depicted in Figure 21.3, if a cracker breaks into the packet filter, the bulk of the internal network is still reachable only through the proxy server. If the proxy server is configured properly, this will present a new set of challenges to the cracker.

It’s also possible to tie the packet filter into the main internal network, and use its filtering rules to direct all traffic to the proxy server. In this case, though, if a cracker breaks into the packet filter and gains root access, there’s nothing to prevent direct attacks on internal computers, completely bypassing the proxy server.