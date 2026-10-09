```
 [!] -destination address[/mask] -d or -dst Matches if the packet is going to address. The address should be an IP address and not a name because, when the system boots, iptables starts before the network and will not be able to resolve a name. See page 483 for formats of the optional mask (only with an IP address).
 [!] -in-interface iface[*] -i For the INPUT, FORWARD, and PREROUTING chains, matches if iface is the name of the interface the packet was received from. Append a plus sign (+) to iface to match any interface whose name begins with iface. When you do not specify in-interface, the rule matches packets coming from any interface.
 [!] -out-interface iface[*] -o For the OUTPUT, FORWARD, and POSTROUTING chains, matches if iface is the interface the packet will be sent to. Append a plus sign (+) to iface to match any interface whose name begins with iface. When you do not specify out-interface, the rule matches packets going to any interface.
 [!] -fragment -f Matches the second and subsequent fragments of fragmented packets. Because these packets do not contain source or destination information, they do not match any other rules.
```

# DISPLAY CRITERIA

The following criteria display information. All packets match these criteria.

```
--verbose -v Displays additional output.
--numeric -n Displays IP addresses and port numbers as numbers, not names.
--exact -x When used with -L, displays exact packet and byte counts instead of rounded values.
--line-numbers Displays line numbers when listing rules. These line numbers are also the rule numbers that you can use in rule match criteria (page 915).
```

# MATCH EXTENSIONS

Rule specification (packet match criteria) extensions, called match extensions, add matches based on protocols and state to the matches described previously. Each of the protocol extensions is kept in a module that must be loaded before that match extension can be used. The command that loads the module must appear in the same rule specification as, and to the left of, the command that uses the module. There are two types of match extensions: implicit and explicit.

# IMPLICIT MATCH EXTENSIONS

Help with extensions Implicit extensions are loaded (somewhat) automatically when you use a --protocol command (described on the next page). Each protocol has its own extensions. Follow the protocol with -h to display extensions you can use with that protocol. For example, the following command displays TCP extensions at the end of the Help output: