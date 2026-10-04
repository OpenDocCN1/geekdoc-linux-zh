# Chapter 16 • Network Architecture

if the traffic is allowed through the rule-base). In this circumstance, the user has actually opened a connection with the firewall and not the host behind it. This is exactly the opposite of the stateful firewalls and is part of the reason why this technology cannot keep up with the speed of the stateful engines.

Some examples of application or proxy devices use Symantec's Raptor (http://enterprisesecurity.symantec.com), TIS Gauntlet (www.tis.com), and Microsoft's ISA Server, now owned by Secure Computing (www.microsoft.com/isa).

The advantages of proxy firewalls include the following:

+   - They provide a more detailed look at the contents of each packet.
- They are not vulnerable to IP spoofing techniques.
- They can confuse attackers because the firewall responds to all ports.

The disadvantages of proxy firewalls include the following:

+   - They are much slower than packet filtering firewalls.
- They are difficult to implement on internal segments.
- You need to create a new proxy for each service you want to pass.

# Throughput and Bandwidth Considerations

Choosing the wrong type of firewall for the internal segment can have some large performance impacts. On the perimeter, your traffic is rarely transferred at 100MB speeds; however, internally this is not the case. Today most networks are switched 100MB/s or even 1Gb/s segments. With this being, implementing a slow or underpowered firewall can have grave consequences on the user's network performance.

Two areas of concern (outside of raw packet throughput) when you place a firewall using session management and Network Address Translation (NAT) tables. As you recall, stateful packet inspection firewalls keep records, or state, each TCP session that it forwards. Even though subsequent packet is not inspected (since it belongs to a session that was already approved), the firewall must still keep track of the session until a host breaks down. This can become a problem when a subnet is generating a lot of traffic that must be forwarded out of the local segment because the state table could reach capacity. When this happens, sessions begin to drop and users will have intermittent network problems.

![](bbox=[0.068, 0.943, 0.293, 0.969])