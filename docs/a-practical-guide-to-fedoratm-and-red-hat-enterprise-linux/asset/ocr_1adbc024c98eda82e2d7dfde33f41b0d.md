The first line that works with the INPUT chain uses --m to specify the state module and accepts ESTABLISHED and RELATED packets:

```
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

The next line accepts all ICMP packets:

```
-A INPUT -p icmp -j ACCEPT
```

This line accepts packets from the local interface:

```
-A INPUT -i lo -j ACCEPT
```

This line allows new TCP connections on port 22 (ssh):

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

These lines reject all packets that have not been accepted and return ICMP error icmp-host-prohibited to the system that sent the packet:

```
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
```

mDNS Running system-config-firewall (see the previous section), added the rule that accepts TCP packets on port 22 and removed the default rule that accepts multicast DNS (mDNS; www.multicastdns.org) packets:

```
-A INPUT -d 224.0.0.251/32 -p udp -m state --state NEW -m udp --dport 5353 -j ACCEPT
```

COMMIT executes the preceding commands. With the preceding rules loaded, you can use iptables to list the rules and see the defaults that iptables puts in place:

```
# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere            anywhere            state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere            anywhere
ACCEPT     all  --  anywhere            anywhere
ACCEPT     tcp  --  anywhere            anywhere            state NEW tcp dpt:ssh
ACCEPT     all  --  anywhere            anywhere            reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere            anywhere            reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

# SHARING AN INTERNET CONNECTION USING NAT

Many scripts that set up Internet connection sharing using iptables are available on the Internet. Each of these scripts boils down to the same few basic iptables commands,