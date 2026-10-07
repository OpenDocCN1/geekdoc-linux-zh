The nat table has two chains: PREROUTING for incoming interfaces and POSTROUTING for outgoing interfaces.

This option affects an entire table:

| -t | Names a specific table to act upon. |
|---|---|
| -t | Names a specific table to act upon. |

These options affect an entire chain:

| -N | Create a new chain. |
|---|---|
| -X | Delete an empty chain. |
| -E | Rename a chain. |
| -P | Change the policy for a built-in chain. |
| -L | List the rules in a chain. |
| -F | Flush the rules out of a chain. |
| -Z | Zero the packet and byte counters on all rules within a chain. |

These options affect rules within a chain:

| -A | Append a new rule to a chain. |
|---|---|
| -I | Insert a new rule at some position within a chain. |
| -R | Replace a rule at some position within a chain. |
| -D | Delete a rule at some position within a chain if passed a numeric value or delete the first rule that matches if passed a rule to match. |

Now let’s look at the sample rules we used with IP Chains above, rewritten in IP Tables syntax.

This rule drops all packets from 192.168.0.11:

```
`iptables -A INPUT -s 192.168.0.11 -j DROP`
```

This rule drops all packets that are not from 192.168.0.11:

```
`iptables -A INPUT -s !192.168.0.11 -j DROP`
```

This displays a list of all rules for the input chain:

```
`iptables -L INPUT`
```

To list the rules in the nat table, add the -t flag instead of a chain name.

```
`iptables -L -t nat`
```

Both of the following rules delete the seventh rule in the input chain, the first by matching the rule number and the second by matching the rule itself:

```
```
iptables -D INPUT 7
iptables -D INPUT -s 192.168.1.11 -j DROP
```
```

Finally, this rule flushes the input chain:

```
`iptables INPUT -F`
```

To flush the rules of the nat table only: