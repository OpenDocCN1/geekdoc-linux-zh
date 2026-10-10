If a locally destined packet is accepted by the **INPUT** chain’s rules, the packet is delivered locally. If a remotely destined packet is accepted by the **FORWARD** chain’s rules, the packet is sent out the appropriate interface.

Outgoing packets from local processes are passed to the **OUTPUT** chain’s rules. If the packet is accepted, it is sent out the appropriate interface. Thus, each packet is filtered once (except for loopback packets, which are filtered twice).

# # Basic iptables Syntax

Firewalls built with Netfilter are built through the iptables firewall administration command. The iptables command implements the firewall policies that you create and manages the behavior of the firewall. Netfilter firewalls have three individual tables: filter, NAT, and mangle. Within these tables, firewalls are built through chains, with each individual link in the chain being an individual iptables command.

Within the default **filter** table there is a chain for input or data coming into the firewall, a chain for output or data leaving the firewall, a chain for forwarding or data being sent through the firewall, and other chains including chains named and configured by the user, commonly (and appropriately) called user-defined chains. The NAT and **mangle** tables have specialty chains that will be discussed later. For now, it’s sufficient to know that the **filter** table is the default table for implementing a basic firewall, the NAT table is used to provide NAT and related functions, and the **mangle** table is used when the packet will be altered by the firewall.

iptables commands are issued with very specific syntax. Many times, the ordering of the options given to iptables makes the difference between a successful command and a syntax error. The commands issued to iptables fall through, so a command that allows certain packets that follows a command that denies those same packets will cause the data to be dropped by the firewall.

The basic syntax for an iptables command begins with the iptables command itself, followed by one or more options, a chain, a set of match criteria, and a target or disposition. The layout of the command largely depends on the action to be performed. Consider this syntax:

```
iptables <option> <chain> <matching criteria> <target>
```

In building a firewall, the option is usually -A to append a rule onto the end of the ruleset. Naturally, there are several options depending on the target and the operation being performed. This chapter covers most of those options.

As previously stated, the chain can be an input chain, an output chain, a forwarding chain, or a user-defined chain. In addition, the chain might also be a specialty chain contained in the NAT or **mangle** tables.