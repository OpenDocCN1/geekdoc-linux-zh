processes running, and this provides the best security. If a server service is required, make sure it is secured properly. If the service is inherently insecure, such as Telnet or the Berkeley r tools, replace them with secure alternative such as SSH.

# ## Blocking unwanted connections with IP chains

Linux has a package called *IP chains* that allows you to set up a firewall on a Linux system. This capability is useful for protecting an entire network at its entry point or blocking certain connections on an individual workstation. When a network interface receives a packet, it puts the packet through a chain of rules. These rules are made up of evaluations that decide if a packet is denied, if it is allowed through, or if the default action is taken.

These chains and rules are configured using the *ipchains* tool. The syntax for *ipchains* is as follows:

```
```
ipchains -[ADC] chain rule-specification [options]
ipchains -[RI] chain rulenum rule-specification [options]
ipchains -D chain rulenum [options]
ipchains -[LFZNX] [chain] [options]
ipchains -P chain target [options]
ipchains -M [ -L | -S ] [options]
```
```

The *ipchains* tool can take many command-line options and parameters. They are broken up into Tables 17-12 and 17-13 for ease of reading and to separate the different functionalities.

**Table 17-12\nipchains Commands**

| Command | Function |
| :--- | :--- |
| *-A, --append* | Appends a rule to the end of the specified chain. |
| *-D, --delete* `&lt;rule number&gt;` `&lt;matching rule&gt;` | Deletes one or more rules from the specified chain. |
| *-R, --replace* `&lt;rule number&gt;` | Replaces the specified rule with another. |
| *-I, --insert* `&lt;number of rule to insert before&gt;` | Inserts a new rule before the specified rule. |
| *-L, --list* `[chain name]` | Lists the rules in the specified chain, or all chains. |
| *-F, --flush* `&lt;chain name&gt;` | Clears all rules in the specified chain. |
| *-Z, --zero* `&lt;chain name&gt;` | Zeroes all counters in the specified chain. |
| *-N, --new-chain* `&lt;chain name&gt;` | Creates a new user-defined chain with the specified name. |