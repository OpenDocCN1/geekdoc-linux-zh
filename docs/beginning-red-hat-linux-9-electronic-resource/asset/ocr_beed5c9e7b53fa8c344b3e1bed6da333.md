# # Security

Rules are grouped together into **chains**. There are three default chains:

+   - 	INPUT, which handles incoming network packets destined for processes on the local machine
+   - 	OUTPUT, which handles outgoing network packets produced by the local machine
+   - 	FORWARD, which handles packets that arrive on one interface and leave on another (i.e. the local machine is forwarding them).

There may be other user defined chains too.

To set up our machine to meet the above specification, we'll clear out (or **flush**) the existing rules with the following command:

```
# iptables -F
```

*We can use this command to delete the named user-defined chain:*

```
# iptables -X name
```

We're going to be dealing only with packets coming into our machine in this example, so we'll be configuring rules in the INPUT chain. Our first step is to configure the default behaviors -- or Policy -- for the INPUT chain so that if it receives a packet that doesn't match any rules, it drops (discards) it. This is the most security conscious approach, as it means that everything is blocked unless we explicitly allow it. The command to set the policy on the INPUT chain to DROP is:

```
# iptables -P INPUT DROP
```

As soon as we type that in, all incoming network packets are dropped, so before we do so, we'd better make sure that we're logged in to the machine on the console. If not, then we'll lose our connection to the machine and won't be able to get it back!

> *We could also have used REJECT instead of DROP as the policy. This would result in a message being sent back to the sender of a blocked packet informing them that the port is not reachable. This is polite, and could prevent a hapless user from continually retrying a connection attempt that will never work. However, it also confirms our presence to a would-be hacker. The policy of DROP silently discards the incoming packet, so our would-be hacker won't even know there's anything listening at our IP address. Of course, this is only valid if we never respond to any requests -- once you've responded to one, you've given the game away.*