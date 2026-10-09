# # The ipchains Program

The *ipchains* program is a Linux tool for managing packet filtering on a Linux server. Support for *ipchains* is compiled directly into the Linux kernel, where the *ipchains* tool inserts and deletes rules from *iptables*. These rules define whether packets are permitted or denied from being sent or received by a Linux system.

![](bbox=[0.73, 0.1, 0.91, 0.17])

![](bbox=[0.05, 0.19, 0.72, 0.49])

*Figure 14-16: A list of all the rules in the IP chains*

# ## iptables and ipchains

One of the differences between *ipchains* and *iptables* is that *iptables* can be configured to be a stateful packet filter. With an *iptables*, the headers within a packet are examined against a known set of rules (the chain) in sequence. If the packet matches a rule, a decision is made for that packet based on what is specified (the target). If a match is not found, then the packet is examined against the next rule in the sequence. This continues until all the rules are exhausted. At this point, *iptables* look to *ipchains* to make the default policy decision.

Each *iptables* contains specific chains. The filter table contains the INPUT, OUTPUT, and FORWARD chains. The *nat* table contains the PREROUTING, POSTROUTING, and OUTPUT chains and is used on networks where only outgoing packets have to be filtered. The *mangle* table contains the INPUT, OUTPUT, FORWARD, PREROUTING, and POSTROUTING chains and is used on large networks where both incoming and outgoing packets have to be filtered.

# ## Syntax

To check your installation for *ipchains*, use the command `rpm -q iptables`.

# ## Use of ipchains

*ipchains* are used to block access to privileged ports of a Linux server. By blocking access to all incoming traffic, an administrator can prevent network access to a Linux workstation connected to a network.