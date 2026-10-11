# CHAPTER SUMMARY

The **iptables** utility creates firewalls intended to prevent unauthorized access to a system or network. An **iptables** command sets up or maintains in the kernel rules that control the flow of network packets; rules are stored in chains. Each rule has a criteria part and an action part, called a target. When the criteria part matches a network packet, the kernel applies the action from the rule to the packet.

Chains are collected in three tables: Filter, NAT, and Mangle. Filter, the default table, DROPs or ACCEPTs packets based on their content. NAT, the Network Address Translation table, translates the source or destination field of packets. Mangle is used exclusively to alter TOS (type of service), TTL (time to live), and MARK fields in a packet. The connection tracking machine, which is handled by the **conntrack** module, defines rules that match criteria based on the state of the connection a packet is part of.

In an emergency you can give the following command to unload all **iptables** modules from the kernel and set a policy of DROP for all tables:

```
# /sbin/service iptables panic
```

# EXERCISES

+   How would you remove all **iptables** rules and chains?

+   How would you list all current **iptables** rules?

+   How is configuring **iptables** different from configuring most Linux services?

+   Define an **iptables** rule that will reject incoming connections on the TELNET port.

+   What does NAT stand for? What does the NAT table do?

# ADVANCED EXERCISES

+   What does the **conntrack** module do?

+   What do rule match criteria do? What are they used for?

+   What do packet match criteria do? What are they used for?

+   Which utilities copy packet filtering rules to and from the kernel? How do they work?

+   Define a rule that will silently block incoming SMTP connections from spmr.com.