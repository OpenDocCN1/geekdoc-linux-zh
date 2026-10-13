# ADDING A RULE

A rule can be added using the -A (append), -I (insert), and -R (replace) options. For the ipchains command. A rule specifies a set of conditions a packet must meet. For example, to deny all ping packets coming from the IP address `10.0.0.1`, add the following rule to the input chain:

```
```bash
# ipchains -A input -s 10.0.0.1 -p icmp -j DENY
```
```

Here -A input indicates that the rule should be appended to the input chain, -s 10.0.0.1 specifies the source address to which the rule applies, -p icmp specifies the protocol of packets to which the rule applies, and -j DENY indicates that when packets match this rule, ipchains should jump to a target named DENY.

You can verify that this rule has been added to the input chain by listing rules in the input chain as follows:

```
```text
# ipchains -n -L input
Chain input (policy ACCEPT):
target     prot opt     source               destination          ports
DENY       icmp - -----  10.0.0.1            0.0.0.0/0             any -> *
```
```

# DELETING A RULE

A rule can be deleted in one of two ways: by specifying the exact rule number in the chain or by specifying the exact rule. If we know the rule we want to delete is the first rule in the input chain, we can delete it with the following command:

```
```bash
# ipchains -D input 1
```
```

Alternately, if we know the rule definition we can delete the rule in the same way we appended a rule while replacing the -A flag with -D. For example, the following command deletes the rules we previously appended to the input chain:

```
```bash
# ipchains -D input input -s 10.0.0.1 -p icmp -j DENY
```
```

# SPECIFYING SOURCE AND DESTINATION IP ADDRESSES

Source or destination IP addresses can be specified in rules in several ways:

+   - As simple IP addresses as in the case of `10.10.10.1`.
+   - As a combination of an IP address and a network mask as in the case of `10.10.10.1/255.255.255.0`.
+   - As a combination of an IP address and the number of bits which belong to the network portion of the address as in `10.10.10.1/24`.

To specify any and all IP addresses, the address and network mask combination should be specified as `0.0.0.0/0` or `0.0.0.0/0.0.0.0`.