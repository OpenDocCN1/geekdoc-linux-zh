| Option | Function |
|---|---|
| -A chain | Appends a rule to a chain. |
| -D chain [rulenum] | Deletes matching rules from a chain. Deletes rule rulenum (1 = first) from chain. |
| -I chain [rulenum] | Inserts in chain as rulenum (default 1 = first). |
| -R chain rulenum | Replaces rule rulenum (1 = first) in chain. |
| -L [chain] | Lists the rules in chain or all chains. |
| -E [chain] | Renames a chain. |
| -F [chain] | Deletes (flushes) all rules in chain or all chains. |
| -R chain | Replaces a rule; rules are numbered from 1. |
| -Z [chain] | Zero counters in chain or all chains. |
| -N chain | Creates a new user-defined chain. |
| -X chain | Deletes a user-defined chain. |
| -P chain target | Changes policy on chain to target. |

TABLE 20-4 IPtables Commands

output device and can be used only for OUTPUT and FORWARD chains. Table 20-5 lists several basic options.

# ## IPtables Options

The IPtables package is designed to be extensible, and there are number of options with selection criteria that can be included with IPtables. For example, the TCP extension includes the `--syn` option that checks for SYN packets. The ICMP extension provides the `--icmp-type` option for specifying ICMP packets as those used in ping operations. The limit extension includes the `--limit` option, with which you can limit the maximum number of matching packets in a specified time period, such as a second.

In the following example, the user adds a rule to the INPUT chain to accept all packets originating from the address 192.168.0.55. Any packets that are received (INPUT) whose source address (`-s`) matches 192.168.0.55 are accepted and passed through (`-j ACCEPT`):

```
iptables -A INPUT -s 192.168.0.55 -j ACCEPT
```

# ## Accepting and Denying Packets: DROP and ACCEPT

There are two built-in targets, DROP and ACCEPT. Other targets can be either user-defined chains or extensions added on, such as REJECT. Two special targets are used to manage chains, RETURN and QUEUE. RETURN indicates the end of a chain and returns to the chain it started from. QUEUE is used to send packets to user space.

```
iptables -A INPUT -s www.myjunk.com -j DROP
```