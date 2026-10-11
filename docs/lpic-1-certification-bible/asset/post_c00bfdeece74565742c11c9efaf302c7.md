
Table 17-12 (continued)

| Command | Function |
| :--- | :--- |
| -P, --policy | Sets the default target for a chain. |
| -M, --masquerading | Used with the -L function, lists the current masqueraded connections. Used with the -S option, sets the kernel masquerading parameters. |
| -S, --set tcp tcpfin udp | Changes the timeout values used for masquerading. The timeouts are as follows: tcp indicates TCP session timeout; tcpfin indicates TCP session timeout after receiving a FIN packet; and udp indicates UDP packet timeout. This option is only used along with the -M flag. |
| -C, --check | Checks the given packet against the selected chain. Useful for testing and debugging. |
| -h | Help. |

Table 17-13
ipchains Parameters

| Option | Function |
| :--- | :--- |
| -p, --protocol [i] | The protocol of the rule or packet to check. Possible values are tcp, udp, icmp, or all. Other values listed in /etc/protocols may be used. A ! preceding the protocol name inverts the test. For example, a rule with !tcp would apply to any protocol that is not tcp. |
| -s, --src, --source [i] address[/mask] [i] [port[:port]] | Specifies the source address and optional port of a connection. |
| --sport, --source-port [i] [port[:port]] | Used to separately define a source port or range of ports. |
| -d, --dst, --destination [i] address[/mask] [i] [port[:port]] | Specifies the destination address and optional port of a connection. |
| --dport, --destination-port [i] [port[:port]] | Separately specifies the destination port. |
| --icmp-type [i] <typename> | Checks for ICMP type. Use -h icmp to see the full list. |

| Option | Function |
| :--- | :--- |
| -J, --jump <target> | Specifies the target of a rule or what to do if a packet matches this rule. If this option is left out of a rule, the rule has no effect but can be used for logging purposes. |
| -i, --interface [!] <interface name> | Specifies the interface through which a packet must enter for the Input chain or exit for the Output chain. |
| [1] -f, --fragment | Specifies that the rule is used only for the second and subsequent fragments of a packet. |
| -b, --bidirectional | Matches the packet in both directions. It is the same as adding two rules with the source and destinations reversed. |
| -v, --verbose | Enables verbose output for the -L command. |
| -n, --numeric | Shows addresses in numeric form, instead of resolving to hostnames. |
| -l, --log | Enables logging for packets that match this rule. |

## Chains and rules

When packets pass through the selected interface, they are evaluated against *rules*. A group of rules makes up a *chain*.

### Chains

There are three main chains in IP chains: Input, Output, and Forward. A packet is processed through the Input chain when it is received by a network interface. The Output chain is used when a packet is sent out a network interface. The Forward chain is used when a packet is being forwarded from one interface to another, inside of a system.

In most cases you put your rules on the Input chain, since this provides the most protection. The chains are processed sequentially: When a packet is received, it goes through the Input chain; if it passes through that, it goes to the Forward chain; and if it survives that, it finally goes to the Output chain. If a packet is destined for the local system it will pass through only the Input chain.

The chains have a default policy that you set up. Normally, the default is `DENY`, and you must explicitly allow things through. The possible default policies are `DENY`, `REJECT`, and `ACCEPT`. A subtle but very important difference exists between `DENY` and `REJECT`. When a packet is met with `DENY`, it is simply dropped. No word is sent back to the source informing it of this action. The `REJECT` policy sends back an ICMP message to the source telling it that the packet was denied. The choice of which to use depends on the situation. Most people want their firewall to silently drop the packet and not report back any information to someone probing their site. The problem with this practice, however, is that it can sometimes cause confusion when troubleshooting a network problem.

## Rules

Rules control what happens to a packet as it passes through a chain. Rules are made up of a condition that must be met and an optional target. When a packet is processed through a chain, it is matched against the rules in order until the first match is found. Once the match is found, the target is invoked, and the packet may then be forwarded along or rejected.

In some cases creating a rule that has no target is useful. This causes the packet to match, but no action is taken, and the packet continues through the chain. The idea is to use these phantom rules for logging and statistical purposes so you can see what type of traffic is being sent through the firewall.

The six basic targets that can be used in rules are as follows:

- ACCEPT
- DENY
- REJECT
- MASQ
- REDIRECT
- RETURN

ACCEPT is used to move the packet to the next chain or out of the network interface if it succeeds through the Output chain. DENY and REJECT were already discussed and cause a packet to be stopped, with varying results. MASQ is used only in the Forward chain and is discussed later in this chapter.

REDIRECT is used to redirect packets to a local socket, instead of the remote socket in their header. It is used only in the Input chain and finds use in applications such as transparent Web caches and proxies. This way, a user's Web request is sent through the cache without the user's even knowing.

RETURN is really used only in user-defined chains. This causes the packet to return to the calling chain. A user-defined chain is a chain just like Input, Output, and Forward, but has no default policy and is created by the user. It is called just like any other target, but by its name, which is set by the user. User-defined chains are used to increase modularity of complex chain structures. They allow the user to break out certain rule check sequences into other parts for ease of administration.

## Rule order

The order in which rules are applied is extremely important. The target of the first matching rule is used on a packet. If the rules are not in the correct order, you may not get the expected result. Consider the following metarules:

```text
Allow Anyone to WebServer at Port 80
Deny hacker.org to WebServer at Port 80
```

Since the processing of the chain stops at the first matching rule, everyone can get to the `webServer`, even the guys from `hacker.org` you are trying to stop. The rules should be reversed so that specific rules should come before general rules.

### Putting it all together

So now you understand rules, chains, conditions, targets, and rule order. Most likely you currently do not have any rules, but to be safe you should clear out the chains by using the `-F` option. These commands can be entered at the command line manually, but are usually put at the beginning of a configuration script:

```
iptables -F input
iptables -F output
iptables -F forward
```

These commands should usually be at the beginning of *any* `iptables` script, to be safe. The last thing you need are quirky results because of a forgotten rule hanging around. The next step is to set the default policy for all three of the standard chains by using the `-P` option. For example:

```
iptables -P input DENY
iptables -P output ACCEPT
iptables -P forward ACCEPT
```

Most rules happen when a packet enters the system, so by default you deny everything and open the gate for certain packets with rules. To keep things simple, set the other two chains to `ACCEPT`. This may not be the best choice for a complicated setup, so use your judgment in the situation at hand. To make sure your changes worked, list the current state:

```bash
debian:/home/jason# iptables -L
Chain input (policy DENY):
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

Getting in the habit of also using the `-n` option when viewing the rules is a good idea. This option causes the system to display only IP addresses, and not to resolve them to hostnames. With an open resolver resolving names may be fine, but when you start restricting access, you may no longer be able to access DNS fonts, and resolving names causes a very long timeout period.

Now you are ready to create your rules. Right now the system is like Fort Knox—nothing is getting in since the default `Input` chain's policy is set to `DENY`, and no rules are defined to get around that. First, allow the internal interfaces to receive packets. Assume this system has two network interfaces: the internal is `eth0` with a network range of `192.168.1.0/24` and the external is `eth1`. To allow the internal interfaces to receive packets, you would use the following:

```
iptables -A input -i lo -j ACCEPT
iptables -A input -i eth0 -j ACCEPT
```
