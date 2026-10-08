Telnet and SSH sessions are in a gray area. On heavily trafficked routers with many sessions, the state maintenance overhead may be a win by bypassing the firewall inspection. For fairly quiescent sessions, however, it's likely that the connection entry will timeout and be thrown away. The state table entry will be re-created when the next packet comes along, after it has passed the traditional firewall rules.

Table 6.15 lists the options available to the state match extension.

# Table 6.15 state Match Extension

| -m | --match state Option Description |
| --- | --- | --- |
| --state <state><state> | Matches if the connection state is one in the list. Legal values are NEW, ESTABLISHED, RELATED, or INVALID. |

TCP connection state and ongoing UDP exchange information can be maintained, allowing network entries to be filtered as NEW, ESTABLISHED, RELATED, or INVALID.

+   - NEW is equivalent to the initial TCP SYN request, or to the first UDP packet.
- ESTABLISHED refers to the ongoing TCP ACK messages after the connection is initiated, by subsequent UDP datagrams exchanged between the same hosts and ports, and to ICMP echo-reply messages sent in response to a previous echo-request.
- RELATED refers only to ICMP error messages. FTP connections are managed by the additional FTP connection tracking support module. With the addition of that module, the meaning of RELATED is extended to include the secondary connection.
- An example of an INVALID packet is an incoming ICMP error message that wasn't a response to a current session, or an echo-reply that wasn't a response to a previous echo-request.

Ideally, using the ESTABLISHED match allows the firewall rule pair for a series to be collapsed into a single rule allows the first request packet. For example, using the ESTABLISHED match, a web client rule requires allowing only the initial outoing SYN request.

Although a firewall setup might work very well for a small or residential site in most cases, it is unlikely to perform adequately for a larger site or a firewall that handles many connections simultaneously. The reason goes back to the case of state table entry timeouts, in which a state for a quiescent connection is replaced because of table size and memory constraints. The next packet that would have been accepted by the deleted state entry requires a rule to allow the packet, and the state table entry must be rebuilt.

![](bbox=[0.015, 0.968, 0.055, 0.981])