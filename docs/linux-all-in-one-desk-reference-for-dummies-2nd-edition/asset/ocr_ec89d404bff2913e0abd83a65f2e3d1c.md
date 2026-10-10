# Enabling packet filtering on your Linux system

Your Linux system comes with built-in packet-filtering software in the form of something called netfilter that's in the Linux kernel. All you have to do is use the iptables command to set up the rules for what happens to the packets based on the IP addresses in their header and the network connection type.

![](bbox=[0.13, 0.23, 0.21, 0.31])

To find out more about netfilter and iptables, visit the documentation section of the netfilter Web site at www.netfilter.org/documentation.

The built-in packet-filtering capability is handy when you don't have a dedicated firewall between your Linux system and the Internet. This is the case, for example, when you connect your Linux system to the Internet through a DSL or cable modem. Essentially, you can have a packet-filtering firewall inside your Linux system, sitting between the kernel and the applications.

# Using the security level configuration tool

Some Linux distributions, such as Fedora Core and SUSE, include GUI tools to turn on a packet-filtering firewall.

![](bbox=[0.11, 0.5, 0.21, 0.59])

In Fedora Core, you can turn on different levels of packet filtering through the graphical Security Level Configuration tool. To run the tool, log in as root and choose System>Administration>Security Level and Firewall. The Security Level Configuration dialog box appears, as shown in Figure 3-2.

![](bbox=[0.13, 0.73, 0.2, 0.87])

Figure 3-2: In Fedora Core, you can set up packet filtering with this tool.

![](bbox=[0.22, 0.59, 0.53, 0.87])

# Book VI
Chapter 3

Improving Network Security