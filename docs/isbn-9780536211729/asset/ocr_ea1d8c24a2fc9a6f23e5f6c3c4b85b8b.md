Remember that use of the state module allows you to bypass the state firewall rules for ongoing exchanges under normal operation. The standard rules must be included, however, if the state table entry for a connection is recycled or times out.

# INCLUDING BOTH STATIC AND DYNAMIC FIREWALL RULES

Resource limits in terms of scalability and state table timeouts can require that both the static and the dynamic rules are used.The top limit is a selling point with large commercial firewalls.

The scalability issue comes in large firewalls designed to handle 50,000–100,000 simultaneous connections—that’s a lot of state. Resources run out at some point, and connection tracking can’t be done. Either the new connection has to be dropped or the software has to fall back to stateless mode.

There's also the issue of timeouts. Connection state isn't kept forever. Slow and quiescent connections can have their state information easily cleaned out to make room for other active connections. When a packet comes along later, the state information has to be rebuilt. In the meantime, the packet flow has to fall back to stateless mode while the transport stack looks up the connection information and informs the state module that the packet is indeed part of an established exchange:

```
if [ "CONNECTION_TRACKING" = "1" ];
$IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
$IPT -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# Using the state module alone, INVALID will break protocols that use
# bi-directional connections or multiple connections or exchanges,
# unless an ALG is provided for the protocol. At this time, FTP and
# IRC are the only protocols with ALG support.

$IPT -A INPUT -m state --state INVALID -j LOG \
  --log-prefix "INVALID output: *"
$IPT -A INPUT -m state --state INVALID -j DROP

$IPT -A OUTPUT -m state --state INVALID -j LOG \
  --log-prefix "INVALID output: *"
$IPT -A OUTPUT -m state --state INVALID -j DROP
```