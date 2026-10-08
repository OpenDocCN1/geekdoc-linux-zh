operations such as IP masquerading are implemented using the NAT table that holds IP masquerading rules. The mangle table is used for specialized packet changes. Changes can be made to packets before they are sent out, when they are received, or as they are being forwarded. This structure is extensible in that new modules can define their own tables with their own rules. It also greatly improves efficiency. Instead of all packets checking one large table, they access only the table of rules they need to.

IP table rules are managed using the `iptables` command. For this command, you will need to specify the table you want to manage. The default is the filter table, which need not be specified. You can list the rules you have added at any time with the `-L` and `-n` options, as shown below. The `-n` option says to use only numeric output for both IP addresses and ports, avoiding a DNS lookup for hostnames. You could, however, just use the `-L` option to see the port labels and hostnames:

```
`iptables -L -n`
```

> **NOTE** In *IPtables* commands, chain names have to be entered in uppercase, as with the chain names *INPUT*, *OUTPUT*, and *FORWARD*.

# Chains

Rules are combined into different chains. The kernel uses chains to manage packets it receives and sends out. A *chain* is simply a checklist of rules. These rules specify what action to take for packets containing certain headers. The rules operate with an if-then-else structure. If a packet does not match the first rule, the next rule is then checked, and so on. If the packet does not match any rules, the kernel consults chain policy. Usually, at this point the packet is rejected. If the packet does match a rule, it is passed to its target, which determines what to do with the packet. The standard targets are listed in Table 20-2. If a packet does not match any of the rules, it is passed to the chain's default target.

# Targets

A *target* could, in turn, be another chain of rules, even a chain of user-defined rules. A packet could be passed through several chains before finally reaching a target. In the case of user-defined chains, the default target is always the next rule in the chains from which it was called. This sets up a procedure- or function call-like flow of control found in programming languages. When a rule has a user-defined chain as its target, when activated, that user-defined chain is executed. If no rules are matched, execution returns to the next rule in the originating chain.

| Target | Function |
| :--- | :--- |
| ACCEPT | Allow packet to pass through the firewall. |
| DROP | Deny access by the packet. |
| REJECT | Deny access and notify the sender. |
| QUEUE | Send packets to user space. |
| RETURN | Jump to the end of the chain and let the default target process it. |

**TABLE 20-2**  *IPtables Targets*