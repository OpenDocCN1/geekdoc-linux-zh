# FIGURE 30.1 A typical firewall

![](bbox=[0.417, 0.146, 0.783, 0.399])

To support a firewall, the Linux kernel must be compiled with the appropriate options:

+   - Network firewalls
- IP: firewalling
- /proc filesystem

The standard Red Hat kernel supports these options. To determine whether a kernel supports the necessary options, check for the file /proc/net/ip_fwchains; if this file exists, the options are supported.

> T/P firewall documentation states that the kernel option IP: always defragment must be configured. This option can now be enabled dynamically by including the line net.ipv4.ip_always_defrag=1 in the file /etc/sysctl.conf.

# Masquerading

Masquerading is closely related to firewalling, and often a Red Hat system is configured to provide both functions. In masquerading, packets leaving a protected network are rewritten to appear as though originated from the firewall host. Similarly, related packets arriving from outside the protected network are rewritten by the firewall host to specify the actual destination. Masquerading is often used to conceal the identity of hosts within the protected network. For example, hosts within the network can be assigned private IP addresses—such as