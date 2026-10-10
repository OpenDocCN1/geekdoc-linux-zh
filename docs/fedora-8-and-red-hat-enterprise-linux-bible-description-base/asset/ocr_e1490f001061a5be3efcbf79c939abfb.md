# Securing Linux with iptables Firewalls

What is a firewall? In the non-computer world, a firewall is a physical barrier that keeps a fire from spreading. Computer firewalls serve a similar purpose, but the “fires” that they attempt to block are attacks from cracker on the Internet. In this context, a firewall, also known as a *packet filter*, is a physical piece of computer hardware that sits between your network and the Internet, regulating and controlling the flow of information.

The most common types of firewalls used today are filtering firewalls. A filtering firewall filters the traffic flowing between your network and the Internet, blocking certain things that may put your network at risk. It can limit access to and from the Internet to specific computers on your network. It can also limit the type of communication, selectively permitting or denying various Internet services.

For Fedora or RHEL to act as a filtering firewall, you can use the iptables features. The iptables feature replaced ipchains as the default Red Hat Linux firewall several releases ago. With Fedora Core 2, ipchains was dropped altogether. This chapter describes the iptables facility and the Firewall Configuration window for starting out with a simple iptables firewall.

# Using the Firewall Configuration window

When you first installed your Fedora or RHEL system, you were given the opportunity to create a basic iptables firewall for your system. Using the Firewall Configuration window, you can see those settings and modify them further.

If you are not familiar with firewalls in general, or iptables in particular, it can be a bit daunting to start out. To make your start with iptables easier for new users, Fedora and RHEL systems offer the Firewall Configuration window. Look through the settings on this window, and then refer to other iptables descriptions that follow for more details on each feature.

To open the Firewall Configuration window, from the System menu select Administration → Firewall (or type *system-config-firewall*). Figure 14-1 shows an example of this window.

You can Enable or Disable the firewall using the radio buttons on the Firewall Configuration window. If you are connected to the Internet or other public network, I strongly suggest you enable your firewall. Even if you are on a trusted LAN you should turn the firewall on, but possibly open some services you might not expose to the Internet (such as NFS and Samba). If the firewall is enabled, select from the following topics in the left column to configure your firewall: