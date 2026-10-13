IP tables support is what netfilter is all about. If you don’t choose this, you won’t be able to run netfilter:

```
IP tables support (required for filtering/masq/NAT)    required
```

The limit option will build support that can be used to limit the number of duplicate messages logged on your logs don’t overflow from hundreds of thousands of duplicate messages. If you do any logging at all, you’ll want this option:

```
limit match support                              optional
```

The new netfilter allows for all kinds of ways to filter packets, including by MAC address. Obviously, this is only effective against hosts to which you are directly connected (that is, there’s no router between them and you). But if someone likes to put their personal laptop on your network using their desktop system’s IP, this option can prevent them from using your Internet connection:

```
MAC address match support                         optional
```

The netfilter MARK option will permit you to use netfilter to mangle packets and mark them for special routing, queuing, or logging. If you have special needs, you might want to include this:

```
netfilter MARK match support                         optional
```

The multiple port match support permits a range of ports to be used in an iptables rule rather than just one port. This can reduce the number of individual rules and provide more flexibility:

```
Multiple port match support                          optional
```

If you want to prioritize packets based on the TOS (which can also be set using netfilter), you’ll need this option:

```
TOS match support                                     recommended
```

Netfilter can recognize and work with a connection state if this option is chosen. Connection states include new, established, related, and unknown. If you want to use the stateful features of netfilter, you’ll need this option:

```
Connection state match support                       recommended
```

Unclean match support applies to any packet not related to an established connection that appears to be other than a new connection. This can be invalid packets, or reply packets for which netfilter knows of no related, established connection, to include ICMP echo replies for which no echo request was sent, or SYN-ACK packets for which no SYN packet was sent. You’ll almost certainly want this option:

```
Unclean match support (EXPERIMENTAL)                  recommended
```

The owner match support permits packets generated locally (on the localhost only) to be matched for user, group, session, or process. This module is only of use if the localhost is to be used as a workstation:

```
Owner match support (EXPERIMENTAL)                   optional
```