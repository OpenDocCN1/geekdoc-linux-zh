# Chapter 24 ✦ Implementing Firewalls in SUSE Linux 619

previously, if you wanted to allow an incoming connection to SSH on the firewall, you would have to first allow the incoming connection and return the traffic from the SSH server to the client. With stateful firewalls, you can tell the firewall to manage the subsequent outgoing connection automatically because it is aware that an incoming connection to the machine will produce traffic in the opposite direction. It does this by storing the state of a connection and acting upon it with connection tracking.

To enable the stateful connection tracking, you need to enable states in the firewall. We discuss this in a small firewall script later in the chapter.

# Setting Your First Rules

Before you touch setting up specific rules, you need to set the default policy for the firewall (see Listing 24-2).

# 24-2: Setting Initial Firewall Rules

```
bible:- # iptables -P INPUT
bible:- # iptables -P OUTPUT
bible:- # iptables -P FORWARD
bible:- # iptables -A INPUT -m state --ESTABLISHED,RELATED -j ACCEPT
bible:- # iptables -A FORWARD -m state --ESTABLISHED,RELATED -j ACCEPT
bible:- # iptables -A OUTPUT -m state --NEW,ESTABLISHED,RELATED -j ACCEPT
```

Here you set the default policy for all chains to drop the packets. In this moment in time, all network connections, regardless of their originating address, will dropped.

To set or change the policy of a chain, you need to specify that this is a policy edit (-P), chain (INPUT, OUTPUT, or FORWARD), and also what to do with the packet.

It's a secure feeling knowing that any connection from the Internet is not needed and the sender has to wait for a timeout before being notified. Imagine running a port scan of all 64,000 available ports on a TCP/IP machine. If they have to wait for a timeout each one, it will take them a few hours to complete the full scan. It provides a kind of tar pit for any malicious users.

This is also true for internal connection, too. If your users are interested in what they can and cannot connect to, without reading the network rules, then they will wait, one hopes, to push them from the network too hard.

You have also configured the stateful firewall with the -m state declaration. This tells the firewall that you will allow any established or related connections on the INPUT chain.