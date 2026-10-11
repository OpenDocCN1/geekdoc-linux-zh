![](bbox=[0.15, 0.08, 0.93, 0.51])

# Figure 17-13 Updating the system

You should also implement a host-based firewall to protect your Linux system. Let’s discuss how this is done next.

# Implementing a Firewall with iptables

Today, most organizations connect their corporate networks to the Internet. Doing so enhances communications and provides access to a wealth of information. Unfortunately, it also exposes your network to a serious security threat. If your users can go out on the Internet, then an uninvited person from the Internet can also get into your network unless you take measures to keep this from happening. To do this, you need to implement a network firewall as well as host-based firewalls on each system.

A network firewall is very different from a host-based firewall. A host-based firewall controls traffic in and out of a single computer system. A network firewall, on the other hand, is used to control traffic in and out of a network segment or an entire network.

In this part of the chapter, we’re going to spend some time learning how to use Linux in both capa cities. We’ll discuss the following topics:

+   - How firewalls work
+   - Implementing a packet-filtering firewall

Let’s begin by discussing how firewalls work.