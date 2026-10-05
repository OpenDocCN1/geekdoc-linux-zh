# Glossary

type specifies the parameters of the admission control; for example:

+   1. Best Effort—has no parameters (beyond source plus destination address, ToS, and precedence).
2. Controlled Load—Specifies a contract that looks to the source (sink) like a lightly loaded network with the specified mean rate. The borrowing of capacity between a flow that has a burst at a higher rate and ones that are currently at a lower rate is possible. The control of this over the short time frame is a factor in selecting a scheduling algorithm (see schedule).
3. Guaranteed Service—This is very much like the ATM CBR contract, but it is also like the VBR rate—it specifies delay bounds and well as throughput parameters. These are actually implemented end-to-end and hop-by-hop, so are somewhat different from the CDV parameter that is a traffic behavior specification than a contract request.
4. Slack—A term in RSVP for divvy up variation along the hops of a path.
5. Controlled Delay—This and the next two parameters are proposed service contracts.
6. Committed Rate.
7. Predictive.

**Classifier.** An implementation of a rule to decide the provenance of a packet and assign it to a class.

**Congestion.** A state of the network and its offered load where traffic is partially or largely not being carried usefully—for example, traffic flows across a link to a bottleneck, only to be dropped. In multiservice networks with reservations, can refer to high call blocking probability—actually, this is simply scarcity of resource.

**Crankback.** A technique where a flow setup is recursively backtracked along the partial flow path to the first node that can determine an alternative path to the destination.

**CSMA (Carrier Sense Multiple Access).** Building block for shared media network mediation.

**CSZ (Clark, Shenker, and Zhang).** Alternative model to CBQ.
**cwnd** (congestion window). This is an important parameter in the TCP congestion avoidance algorithm discussed in Chapter 7.

**Daemon.** Always on UNIX user-space process that handles various service requests and enhances kernel level functionality.

**Datagram.** An IP packet.
DECnet. The Digital Equipment Corporation's old network architecture.