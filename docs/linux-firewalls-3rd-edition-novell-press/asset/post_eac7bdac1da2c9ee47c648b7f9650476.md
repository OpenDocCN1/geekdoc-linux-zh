
## UDP Services: Place Incoming Packet Rules After Spoofing Rules

Use of the state module also allows the rule for the remote client's incoming connection request, the initial SYN packet, to be logically separate from the rule for the client's subsequent ACK packets. Only the initial connection request, the initial NEW packet, needs to be tested against the spoofing rules.

Without the state module, for UDP-based services the rule for incoming packets must always follow the spoofing rules. The concept of client and server is maintained at the application level, assuming that it's maintained at all. At the firewall and UDP levels, without connection state, there is no indication of initiator and responder, other than the service port or unprivileged port used. As you saw in Chapter 4, some UDP services use the associated well-known service port for both the client and the server, whereas other services use unprivileged ports for both.

DNS is an example of a connectionless UDP service. Without connection state, there isn't a mapping between the destination address where the client sent a query and the source address in an incoming response packet. One of the reasons DNS cache poisoning is possible is that DNS server implementations do not check whether an incoming packet was a legitimate response from the server previously queried or whether the packet was sent from some other address. Furthermore, some implementations do not even ensure that a client made a request. An incoming, unrequested rogue packet could be used to update the local DNS cache even without an initial query having been made.

## TCP versus UDP Services: Place UDP Rules After TCP Rules

Overall, UDP rules should be placed later in the firewall chains, after any TCP rules. This is because most Internet services run over TCP, and connectionless UDP services are typically simple, single-packet query-and-response services. Testing the single or UDP packet or a handful of them against the preceding rules for ongoing TCP connections doesn't add noticeable drag to a UDP query and response. A notable exception is streaming media, such as the RealAudio data stream. However, as stated in Chapter 4, multimedia and other bidirectional, multiconnection session protocols are not firewall-friendly to begin with. Such services cannot pass through a firewall or NAT without specific ALG support.

## ICMP Services: Place These Rules Late in the Rule Chain

ICMP is another protocol whose firewall rules can be placed late in the rule chain. ICMP packets are small control and status messages. As such, they are sent relatively infrequently. Legitimate ICMP packets usually consist of a single, unfragmented packet. With the exception of echo requests, ICMP packets are almost always sent as a control or status message in response to an exceptional outgoing packet of some kind.

### Place Firewall Rules for Heavily Used Services as Early as Possible

Generally, there are no hard-and-fast rules for firewall rule placement in a list. Rules for heavily used services, such as the HTTP-related rules for a dedicated web server, should be placed as early as possible. Rules for applications that involve high, ongoing packet counts also should be placed as early as possible. However, as mentioned earlier, the data stream protocols for applications such as FTP and RealAudio require the rules to be placed near the end of the chain, after any other application rules.

### Use the Multiport Module to Specify Port Lists

Some small gains can be had by using the multiport module to specify port lists, thereby collapsing several rules into one. Both the number of rules in the list and the number of specific match tests performed are reduced. Effectively, the packets matching one of the ports in the list share a single instance of the tests for the interface, protocol, TCP flags, and source and destination address. The actual amount of gain seen is dependent on the specific services the firewall accepts. Obviously, the services represented by the ports must share identical transport header characteristics to share the specific set of tests the rule represents.

### Use Traffic Flow to Determine Where to Place Rules for Multiple Network Interfaces

If the host has multiple network interfaces, rules specific to a given interface should be placed with regard to which interfaces will have the heaviest traffic flow. Rules for those interfaces should precede rules for other interfaces. Interface considerations are probably of little interest to a residential site, but they can have a major impact on throughput for a commercial site.

As a case in point, this issue came up several years ago with a small ISP that had built a firewall based on the ipfwadm and ipchains examples on Bob Ziegler’s website. As shown in Figure 5.1 and Figure 5.2, the path that packets take through the operating system is very different between IPFW and Netfilter. Unlike Netfilter and iptables, with ipchains, packets passing between network interfaces are passed from the input chain to the forward chain to the output chain. The examples on the website were intended as examples for people at home. The input and output rules for the LAN were the last rules in the scripts. The rules specific to the local Linux host come first. The ISP’s firewall was primarily functioning as a router or gateway. Through experimentation, the ISP found that moving the I/O rules for the LAN interface to the beginning of the input and output chains resulted in more than a megabit-per-second increase in throughput.

### FIGURE 5.1
IPFW loopback and masqueraded packet traversal.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_204_0.png)

### FIGURE 5.2
Netfilter packet traversal.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_204_1.png)

## User-Defined Chains

The `filter` table has three permanent, built-in chains: **INPUT**, **OUTPUT**, and **FORWARD**. iptables enables you to define chains of your own, called user-defined chains. These user-defined chains are treated as rule targets—that is, based on the set of matches specified in a rule, the target can branch off or jump to a user-defined chain. Rather than the packet being accepted or dropped, control is passed to the user-defined chain to perform more specific match tests relative to packets matching the branch rule. After the user-defined chain is traversed, control returns to the calling chain, and matching continues from the next rule in the calling chain unless the user-defined chain matched and took action on the packet.

Figure 5.3 shows the standard, top-down rule traversal using the built-in chains.

### FIGURE 5.3
Standard chain traversal.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_205_0.png)

User-defined chains are useful in optimizing the ruleset and therefore are often used. They allow the rules to be organized into categorical trees. Rather than relying on the straight-through, top-down check-off list type of matching inherent in the standard chain traversal, packet match tests can be selectively narrowed down based on the characteristics of the packet. Figure 5.4 shows initial packet flow. After initial tests common to all incoming packets are performed, packet matching branches off based on the destination address in the packet.

Branching is based on destination address in this example. Source address matching is done later in relation to specific applications, such as remote DNS or mail servers. In most cases, the remote address will be "anywhere." Matching on destination address at this point distinguishes between unicast packets targeted to this machine, broadcast packets, multicast packets, and (depending on whether it's the INPUT or FORWARD chain) packets targeted to internal hosts.

Figure 5.5 details the user-defined chain for the protocol rules for packets specifically addressed to this host. As shown, user-defined chains can jump to other user-defined chains containing even more specific tests.
