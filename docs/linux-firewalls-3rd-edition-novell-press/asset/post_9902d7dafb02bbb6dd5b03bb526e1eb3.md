
As a result of modifying addressing information for applications that embed local addresses or ports in the application payload, incoming packets destined to a NAT host must be defragmented before forwarding.

NAT increases resource and performance requirements for NAT devices, which otherwise would be dedicated to fast datagram forwarding. NAT represents not only the overhead of defragmentation, packet inspection, and packet modification, but also the overhead of state maintenance, state timeouts, and state garbage collection.

Because of state maintenance within the network and the associated resource requirements, NAT devices are not infinitely scalable. Additionally, without complicated sharing techniques, hosts cannot use multiple peer NAT devices, an aspect of the single point of failure.

Bidirectional, multicast stream protocols require application-specific NAT support to forward incoming secondary streams to the proper local host. (Note that these protocols generally require ALG support for firewalling as well.)

NAT can break the capability to run multiple instances of the same local network client application in connection with the same remote server. (This problem tends to occur with network games and IRC, where the session has associated incoming streams.)

NAT cannot be used with transport mode IPsec for end-to-end security for a few reasons:

- End-to-end Transport-layer security techniques are not possible because the techniques rely on end-to-end integrity of the packet header contents for authentication.
- End-to-end Transport-layer security techniques are not possible because the techniques rely on end-to-end integrity of the packet's data payload, which also relies on packet header integrity.
- End-to-end Transport-layer security techniques are not possible because data encryption renders the packet's contents unavailable for inspection. NAT modifications are not possible to change embedded address and port information.
- Security trust relationships must be extended into the network from the endpoint hosts, possibly to a point outside the local site altogether. IPsec and most VPN technologies must be extended to the NAT device (in other words, IPsec tunnel mode). Again, the NAT device becomes a single point of failure because the NAT device must terminate the VPN and establish a new link as a proxy to the destination.

iptables provides full NAT functionality, including both source (SNAT) and destination (DNAT) address mapping. The term *full NAT* isn't a formal term; I'm referring to the capability to perform both source and destination NAT, to specify one or a range of translation addresses, to perform port translation, and to perform port remapping. iptables supports the three general types of NAT (traditional NAT, bidirectional NAT, and twic NAT), as defined in RFC 2663.

A partial implementation of NATP, known as masquerading among Linux users, was provided in earlier Linux releases. It was used to map all local, private addresses to the single public IP address of the site's single public network interface.

NAT and forwarding were often spoken of as two components of the same thing because masquerading was specified as part of the forward rule's semantics. Blurring the concepts was irrelevant functionally. Now it's very important to keep the distinction in mind. Forwarding and NAT are two distinct functions and technologies.

*Forwarding* is routing traffic between networks. Forwarding routes traffic between network interfaces as is. Connections can be forwarded in either direction.

*Masquerading* sits on top of forwarding as a separate kernel service. Traffic is masqueraded in both directions, but not symmetrically. Masquerading is unidirectional. Only outgoing connections can be initiated. As traffic from local machines passes through the firewall to a remote location, the internal machine's IP address and source port are replaced with the address of the firewall machine's external network interface and a free source port on the interface. The process is reversed for incoming responses. Before the packet is forwarded to the internal machine, the firewall's destination IP address and port are replaced with the real IP address and port of the internal machine participating in the connection. The firewall machine's port determines whether incoming traffic, all of which is addressed to the firewall machine, is destined to the firewall machine itself or to a particular local host.

The semantics of forwarding and NAT are separated in iptables. The function of forwarding the packet is done in the **filter** table using the **FORWARD** chain. The function of applying NAT to the packet is done in the **nat** table, using one of the **nat** table's **POSTROUTING**, **PREROUTING**, or **OUTPUT** chains:

- Forwarding is a routing function. The **FORWARD** chain is part of the **filter** table.
- NAT is a translation function that is specified in the **nat** table. NAT takes place either before or after the routing function. The **nat** table's **POSTROUTING**, **PREROUTING**, and **OUTPUT** chains are part of the **nat** table. Source NAT is applied on the **POSTROUTING** chain after a packet has passed through the routing function. Source NAT is also applied on the OUTPUT chain for locally generated, outgoing packets. (The filter table OUTPUT chain and the nat table OUTPUT chain are two separate, unrelated chains.) Destination NAT is applied on the PREROUTING chain before passing the packet to the routing function.

A word of caution is in order for readers who are used to the combined forward and MASQ semantics of ipfwadm and ipchains. In iptables, maintaining the clear demarcation between prerouting, forwarding, and post-routing has serious repercussions in terms of the forwarding and NAT rules, as compared to those in ipfwadm and ipchains. In iptables forwarding, the rules are usually specified as a pair, one for each direction between the two interfaces. Use of the state module can hide this fact by allowing all ESTABLISHED rules to be collapsed into a single pair.

In iptables NAT, a single rule is specified. The NAT table entry is created when the first packet in the exchange is received or sent. NAT recognizes returning responses by their destination address and port pair, and it automatically reverses the original process. Because forwarding and NAT are applied on different chains at different points in the packet's path, all three rules are needed: the two rules in the forwarding rule pair and the single NAT rule.

Perhaps a more insidious issue is just what the address in the packet is on any given chain. Associated rules on the PREROUTING, POSTROUTING, FORWARD, INPUT, and OUTPUT chains will see different addresses in the same packet. The various rules applying to the same packet will have to match on different addresses.

> **WHICH DESTINATION ADDRESS IS SEEN WHERE?**
> 
> Destination NAT is applied on the nat table's PREROUTING chain, before the routing decision is made. Rules on the PREROUTING chain must match on the original destination address in the packet's IP header. Rules on the filter table's INPUT or FORWARD chain must match on the modified, NATed address in the same packet header. Likewise, if that same packet were to also have source NAT applied after the routing decision is made, and if the destination address were important to match on, the rule on the nat table's POSTROUTING chain would match on the modified destination address.
> 
> Source NAT is applied on the nat table's POSTROUTING chain, after the routing decision is made. Rules on any chain match on the original source address. The source address is modified immediately before sending the packet on to the next hop or destination host. The modified source address isn't seen on the host applying the source NAT.

None of these distinctions between forwarding and NAT was an apparent issue with ipfwadm and ipchains. The forwarding rule pair wasn't necessary when masquerading. Two-way forwarding and NAT were implied by a single rule. The incoming local interface was implied by the source address. The translated source address was taken from the outgoing public interface specification. Reverse translation for response packets was implied without an explicit rule.

> DON'T GO OVERBOARD USING NAT SYNTAX
> 
> The rest of this chapter presents the nat table syntax. Another word of caution is called for when looking at the complete NAT syntax. The following sections describe the simpler, more general syntax used with NAT, which is what will be used most commonly. The average site won't have a use for the specialized features available in the nat table.
> 
> Both SNAT and DNAT rules can specify the protocol, source and destination addresses, source and destination ports, and state flags, in addition to the translated address and ports. When this is done, the nat table rules look very much like filter table rules. It's very easy to confuse NAT rules with firewall rules, especially for people who are used to ipchains syntax. Actual filtering is done in the FORWARD chain.
> 
> You could mirror the match fields between the FORWARD rules and the NAT rules; the two sets of rules could look nearly identical. For large rule sets, it would quickly become an error-prone, administrative nightmare and would accomplish very little.
> 
> Remember that iptables forwarding and NAT are two completely separate functions. The actual firewall filtering is done by the rules in the filter table. For most people, it's best to keep the nat table rules simple.

## Source NAT

Two forms of source NAT exist in the iptables nat table, specified as two distinct targets, SNAT and MASQUERADE. SNAT is standard source address translation. MASQUERADE is a specialized form of source NAT for use in environments in which an arbitrary, dynamically assigned IP address is assigned on a temporary, connection-by-connection basis.

Both targets are used on the nat table's POSTROUTING chain. Source address modifications are applied after the routing decision has been made to choose the proper outgoing interface. Thus, SNAT rules are associated with an outgoing interface, not with an incoming interface.

### STANDARD SNAT

This is the general syntax for SNAT:

```
iptables -t nat -A POSTROUTING -o <outgoing interface> ... \
-j SNAT --to-source <address>[:<address>][:<port>-<port>]
```
