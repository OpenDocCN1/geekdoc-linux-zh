![](bbox=[0.06, 0.03, 0.23, 0.05])

Before doing that, clear all the existing rules:

```
```bash
echo "Flush existing rules"
/sbin/iptables -F
echo "Set the default policy to drop packets"
/sbin/iptables -P INPUT DROP
/sbin/iptables -P OUTPUT DROP
/sbin/iptables -P FORWARD DROP
```
```

By now, you might have noticed that a rule basically specifies some conditions that the packet must possess. If these conditions are matched, the action specified in the rule is taken; or else the next rule in the chain is checked, and this continues until a rule is matched. If none of the rules in the chain is matched, the default action or policy (here, DROP) is taken.

Let’s write our first rule—a rule to allow outgoing SSH packets from the private network:

```
```bash
echo "Allow outgoing SSH"
/sbin/iptables -A FORWARD -p TCP -i eth0 \
-s 192.168.9.0/24 -d 0/0 -dport 22 -j ACCEPT
```
```

This rule is self-explanatory—well, almost. The option -A specifies the chain to which the rule is to be appended, and -p specifies the protocol (UDP, TCP, ICMP and so on). The option -i names the interface through which the packets will be received. Because the packets are coming from the 192.168.9.0/24 network (the -s specifies the source address) for outgoing SSH packets, it will come through eth0 of the firewall. The destination port (-dport) is 22 for SSH traffic. The destination address is indicated with the -d option, and 0/0 means any address. Finally, the action for such packets that are matched is ACCEPT (specified with the -j option), which means allow the matched packets to go through.

Now, we have written a rule to allow SSH traffic from 192.168.9.0/24 to go anywhere. But, will this work? Will you be able to do an SSH logon from your private network to a machine in the public network? Where have we allowed packets to come from the SSH server (in the public network) back to the client (in the private network)? The following rule achieves that:

```
```bash
/sbin/iptables -A FORWARD -p TCP -i eth1 -s 0/0 \
--sport 22 -d 192.168.9.0/24 -j ACCEPT
```
```

This looks fine, but then we need to write such a rule for every service. Worse, the above rule does more than what is required. It allows any machine to connect to the private network using the source port 22. What we should do instead is append a rule that allows only those packets from the public network that are part of the SSH connections initiated by machines in the 192.168.9.0/24 network.

iptables maintains state information to do such connection tracking. The four states maintained are NEW, ESTABLISHED, RELATED and INVALID. We won’t discuss these states in detail here. For the time being, keep in mind that state NEW indicates the packet is part of a new connection. When a response packet is seen in the reverse direction, the connection becomes ESTABLISHED. Note that this has nothing to do with the states in the TCP connection establishment process. An ICMP or UDP reply for the corresponding requests also will mark the connection as ESTABLISHED. Refer to iptables-tutorial.frozentux.net/iptables-tutorial.html#STATEMACHINE to learn exactly how the connection tracking mechanism works. Now (after removing the above rule), to forward all those packets forming part of the ESTABLISHED connection, we write the following rule:

```
```bash
echo "Allowing ESTABLISHED connections"
/sbin/iptables -A FORWARD -m state --state \
ESTABLISHED -j ACCEPT
```
```

This rule ensures that only packets part of an ESTABLISHED connection will be accepted; a new connection request to 192.168.9.0/24 will not be accepted. Ideally, to access any services (such as HTTP or FTP), we need to allow only NEW and ESTABLISHED connections to go out (NEW will allow the first packet, ESTABLISHED will allow all following packets of the same connection), and only ESTABLISHED connections to come into the private network. Similarly, if you have a DNS server in your network, which has to be permitted access (queried) from the outside, the following rule does that (assuming that 198.168.9.1 is the DNS server):

```
```bash
echo "Allowing incoming DNS requests"
/sbin/iptables -A FORWARD -p TCP -i eth1 \
```
```

![](bbox=[0.07, 0.53, 0.46, 0.95])