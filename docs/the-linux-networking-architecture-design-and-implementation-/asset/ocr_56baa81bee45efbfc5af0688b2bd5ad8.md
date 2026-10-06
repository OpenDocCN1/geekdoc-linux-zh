# Chapter 19 Packet Filters and Firewalls

means that, in addition to the linear processing of rules lists, we can also implement branching. Other possible branch destinations are the following:

+   - ACCEPT—completes processing of the rules list and releases the packet for further handling.
- DENY—discards the packet and returns an ICMP message of the "destination unreachable" to the sender.
- REJECT—(an item with new Linux 2.2) makes sense only for the input chain and directs the packet to another local port. This is useful for, example, transparent proxies, where all HTTP requests are redirected from port 80 to the port of a local HTTP proxy.

This means, if a TCP/IP packet is addressed to the local computer, then it first has to undergo the usual verifications of the checksum field and the packet length before it arrives in the input chain, where it is handled according to this rule list.
Packets belonging to the second class (addressed to computers in a different network) visit all three rules hooked into the kernel in ipchains. As mentioned above, they first arrive in the input chain. The destination address is not in the local computer, so the packet is passed to the forward chain. Before this step, the packet is checked to see whether it is a packet masked by NAT. If this is the case, the packet is unmasked and passed directly to the output chain, bypassing the forward chain. The forward chain accepts the packet, then a final step checks it in the output chain, before it leaves the router. Outgoing packets created in the local computer are handled exclusively by the output chain.
Each rules list has options to log the network traffic it handles. The counters of these functions have 64 bits since Linux Version 2.2; this finer granularity, comparison with that of the 32-bit predecessor versions, prevents overflow. In addition to the core functionality covered by ipchains, the packet-filtering architecture of Linux 2.2 uses additional modules to support more complex protocols, including active FTP (see Section 19.2.1), RealAudio or CUSeMe, which are controlled over additional management tools (e.g., ipmasqd). The entire core functionality is managed by the ipchains program, which is described in more detail below.

# 19.2 The ipchains Rule Syntax

This section describes the ipchains program, which is used to manage rules lists.
The basic structure of a rule definition is given by the following form: ipchains -<operation> <chain> <criterion> <branch destination> -j command-line options of ipchains and iptables, before we describe the options in detail.

Operation: We can use one of the keywords listed in Table 19–1 to specify how we want the entering rules list to be manipulated. We use APPEND to build a list, which means that the new rule we just defined is appended to the end of a list. To generate a user-defined rules list, we use NEW. User-defined rules behave like subfunctions of the respective lists. This means that, when they are,