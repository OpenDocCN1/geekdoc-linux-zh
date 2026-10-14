+   KMyFirewall is a KDE-based program that lets you set up a "personal firewall" or protect a larger network using IP tables. It includes a setup wizard for less experienced users, plus a more advanced interface to help you create complex rules. You can save a copy of your firewall rules to a separate file and then use that file to easily configure other firewalls running KMyFirewall when the same rules should be applied. For information, visit http://kmyfirewall.sourceforge.net.

+   One of the most full-featured firewall configuration utilities for Linux is GuardDog. GuardDog can use either a graphical interface or its own command-line utility. For details, see www.simonzone.com/software/guarddog/.

# Setting up a DNS Name Server

In Chapter 12, "Configuring Networks," you learned how to configure the DNS resolver using configuration files such as /etc/resolv.conf, /etc/hosts, /etc/host.conf, and /etc/nsswitch.conf. In this section you learn how to create a DNS server on Linux on which other systems can rely to resolve host names and IP addresses.

You can think of the information in DNS as an Internet-wide inverted hierarchical tree, as Figure 15-15 illustrates. The very top of the tree is called the root and is represented by a period: "." The root is typically only mentioned in regard to the root name servers—DNS servers that the organizations that run the Internet have designated as a starting point for DNS queries. More commonly, you see the last part of domain names referred to as top-level domains such as .org, .com, .edu, and .net, along with many others.

![](bbox=[0.07, 0.68, 0.92, 0.88])

Figure 15-15 The structure of DNS

To resolve a host name or IP address, a client asks a DNS server for the needed information (for example, "What is the IP address of www.google.com?"). The DNS server can either find another DNS server that has that information already stored (cached), or it can locate the server where the managers of google.com officially defined what the IP address is for their server. Finding the official google.com DNS server takes longer, but the google.com address is cached in many DNS servers, so doing that is rarely needed.