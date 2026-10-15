# Special Input Rules

A normal firewall will not allow a client on the Internet to initiate a connection. All input rules related to the Internet interface have the -k option set (ACK flag must be set in TCP header). This causes two problems, however. The first problem is that if your firewall will be running an SMTP daemon, refusing all SYNC packets will cause the SMTP daemon to hang. If a client on the Internet wants to send you mail via SMTP, the client opens port 25 on your firewall. You can bypass this problem by specifying a special input rule for the SMTP port. The SMTP rule should specify that anybody on the Internet may open a connection to port 25, and only port 25. This rule may look like the following example.

```
# Add input rule for Internet -> me for mail (stops at firewall)
ipfwadm -I -a accept -P tcp -S 0.0.0.0/0 -D 194.109.13.150 25
```

This connection will stop at the firewall, so it does not need an accompanying output or forwarding rule.

# Listing 12.3 Examples of firewall packet filtering rules.

```
# Add output rule for local -> Internet
ipfwadm -O -a accept -P tcp -S 194.109.13.150 -D 0.0.0.0/0
```

This rule defines an output rule for the Internet interface. It states that a packet for any destination on the Internet is allowed out. This rule applies only to packets for the TCP protocol.

```
# Add input rules for cli# Add output rule for local -> Internet
ipfwadm -O -a accept -P tcp -S 194.109.13.150 -D 0.0.0.0/0
```

This rule defines an output rule for the Internet interface. It states that a packet for any destination on the Internet is allowed out. This rule applies only to packets for the TCP protocol.

```
# Add input rules for clients -> Internet (will masquerade)
ipfwadm -I -a accept -P tcp -V 193.78.174.33 -S 193.78.174.34 -D 0.0.0.0/0
ipfwadm -I -a accept -P tcp -V 193.78.174.33 -S 193.78.174.35 -D 0.0.0.0/0
```

This rule describes packets sent by the hosts on the local net to destinations on the Internet. These packets are going to be masqueraded by the forwarding rules. As you can see, these packets must be received on the trusted interface 193.78.174.33 (-V option).

The final example shows you a masquerading rule.

```
# Add forwarding rules for clients
ipfwadm -F -a masquerade -P tcp -S 193.78.174.34 -D 0.0.0.0/0
ipfwadm -F -a masquerade -P tcp -S 193.78.174.35 -D 0.0.0.0/0
```

As you can see, the policy here is masquerade, so these packets will be masqueraded.