```
$IPT INPUT -i INTERNET -p udp \
-s TIME_SERVER --sport 123 \
-d IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

Note that the previous rules are written for a standard client/server UDP communication. Depending on your particular client and server software, it's possible that one or both of them will use the NTP server-to-server communication model, with both the client and the server using UDP port 123.

# 7.7 Filtering ICMP Control and Status Messages

ICMP messages are generated in response to a number of error conditions, and are produced by network analysis programs such as ping and traceroute.

ICMP MESSAGE TYPES AND IPTABLES
iptables supports the use of either the ICMP numeric message type or the alphabetic symbolic name.
iables also supports use of the message subtypes, or codes. This is especially useful for finer filtering control over type 3 Destination Unreachable messages. For example, you could specifically disallow outgoing Port Unreachable messages by disabling an incoming traceroute, or you could specifically allow only outgoing Fragmentation Needed messages.

To see a list of all supported ICMP symbolic names in iptables, run iptables -p icmp -h. To see the official RFC assignments, go to http://www.iana.org/assignments/icmp-parameters.

# 7.7.1 Error Status and Control Messages

Four ICMP control and status messages need to pass through the firewall: Source Quench, Parameter Problem, incoming Destination Unreachable, and outgoing Unreachable of subtype Fragmentation Needed. Other ICMP message types are optional: Echo Request, Echo Reply, other outgoing Destination Unreachable subtypes, and Time Exceeded. Other message types can be ignored, or filtered out by the default policy.

Of the message types that can—or—should ignored, redirect is dangerous because of its role in denial-of-service attacks as a redirect bomb. (See Chapter 5 for more information on redirect bombs.) With redirect, the remaining ICMP message types are specialized control and status messages intended for use between routers.

The following sections describe the message types important to an endpoint host, as opposed to an intermediate router, in more detail.