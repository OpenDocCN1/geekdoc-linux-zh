they would force it to run on a new port number, or perhaps look for an alternative program, I limited the bandwidth by using QoS. In my profile, I specified the port number used and the IPs that were to be restricted, and added the rule for that service to be only one percent of bandwidth utilization. This meant that at any time, only one percent of our network traffic could be used for Napster.

My users were always able to connect to the Napster network, but download speeds were so atrocious that they inevitably gave up. This is obviously a small reason to use ACL; however, it illustrates the practical uses of the technology.

# IDS Configuration and Placement

Intrusion detection systems tend to be the black sheep of computer security industry. Many administrators do not realize the amount of nurturing devices require for them to be an effective part of the overall security model. IDS are plagued with high false-positive rates and large amounts of administrative overhead. However, if you understand these concepts, and are willing to commit to the daily duties, an IDS can fit nicely into your security architecture. The following section will give you a good understanding of how an IDS should be utilized on the internal segments.

# Types of Network and Host IDS

On the internal segments, we are mainly concerned with two types of intrusion detection systems: network- and host-based. Your network architecture should properly defend your resources from malicious users. Network sensors provide a detailed look, in real-time, to the threats that exist on the network, whereas the host-based sensor will confirm the success or failure of the attack on the particular host. Both methods are explored thoroughly in the following sections, including some different products to consider.

# Network-Based Intrusion Detection Systems

Just like the tools mentioned in the earlier section “Learning Your Network’s Security Design,” a network intrusion detection system (NIDS) sits at the lowest level of your network and monitors the traffic as it passes by: Most NIDSs operate through protocol analysis and pattern matching. In other words, the NIDS will watch the traffic as it passes by the wire and compare it against the installed policies and attack signatures. Furthermore, many devices have the capability to not only identify known attack signatures (such as Denial of Service