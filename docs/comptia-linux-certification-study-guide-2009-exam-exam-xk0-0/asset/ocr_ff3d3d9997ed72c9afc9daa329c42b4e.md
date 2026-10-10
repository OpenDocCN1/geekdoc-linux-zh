This command accepts packets entering the system on eth0 from the source network 192.168.1.0/24. The command can be more specific in terms of ports and IP addresses. For instance, to block (deny) all TCP ports from 1 to 1023 leaving the system, the command is

```
ipchains -1A output -l tcp -1 -lsport 1:1023 -lj DENY -11
```

Alternatively, you can also block or allow UDP ports as well such as

```
ipchains -1A output -1p udp -lj DENY -11
```

As you can see, ipchains is very powerful but requires careful setup. Often, applications may use more than one port, and may use one port into a system and another one out. Careful testing of ipchains is therefore required, and documentation of the rules you install is particularly important. Why you blocked or allowed a specific port may be forgotten months after the event.

# iptables

The ipchains program was implemented into Linux from early on and is still in use in early Linux kernels. The Linux kernels 2.4 and 2.6 and later use the iptables program. Like ipchains, iptables is a user space program primarily for system administrators. It is used to configure the tables, rules, and filters to control the treatment of network packets into and out of the system. It uses the Xtables framework, which itself is used by Netfilter. In the majority of Linux systems, the program is installed as /usr/sbin/iptables. Xtables is the kernel-level component and provides an application program interface (API) for kernel-level extensions. The tables are associated with a number of specific kinds of packet processing. Packets are processed by the system by rules in a chain, with each rule able to send the packet to another rule, if necessary. All network packets into and out of the system must traverse at least one chain.

There are three predefined chains for input, output, and forward in the table. A packet traverses the chain until a rule matches the packet and decides what to do with it (such as accept or drop a packet), return the rule processing to the calling chain, or until the end of the chain is reached. The current rules can be displayed using the iptables -L command. The iptables command must be run as root, as it requires elevated privileges. As network address translation (NAT) is configured from the packet filter ruleset, this is included with iptables.

The iptables package includes tables for IPv4 and also IPv6, the later being designated with the table ip6tables. There are also a number of additional programs that work with iptables - the most common being netfilter, whose development team were primarily responsible for the